# 1.2 Install Ubuntu & ROS2 On Jetson-Nano


## 1.Steps of Install and run Ubuntu On Jetson Nano

1.Download Xubuntu-20.04-l4t-r32.3.1.tar.tbz2

2.1.Flash the image to SD cards: download for linux x64 
right click on balena-etcher-electron-1.5.109-linux-x64.zip >> Open With Archive Manager >> Extract Here

2.2.**Open etcher** >> balenaEtcher >> flash from file

2.3.Command to extract the Ubuntu image that has been downloaded :
```
tar -xvjf Xubuntu-20.04-l4t-r32.3.1.tar.tbz2
```
2.4.**Flash from file** >> main/dev/jetson_nano/mages/Xubuntu-20.04-l4t-r32.3.1.img

2.5.**Selecte target** >> connect the storage device >> selecte the device name >> click Select >> Flash >> Type your password

3.1 Following the path of the extlinux.conf on the SD card in case you have a Jetson B01: boot/extlinux/extlinux.conf

if you have the Jetson Nano B01, you have to add the following line in the extlinux.conf:
```
FDT /boot/tegra210-p3448-0000-p3449-0000-b00.dtb
```
3.2. boot/extlinux/extlinux.conf >> right click and Open in Terminal :
```
sudo vim extlinux.conf
```
*NOTE*: To find out which .dtb file is compatible with your Nano run the following on the Nano (e.g. with official Nvidia image):
```
cat /sys/firmware/devicetree/base/compatible
```
This command could also work instead:
```
fdtget /boot/dtb/*.dtb / compatible
```
Finally you could Backing the SD Card >> conecte devices >> usually the LD will Light up

4- define how much space you want to give to your APP Partition.


## 2.Steps of Install and run ROS2 On Jetson Nano

**set the local** by write the following command in the Terminal :
```
locale %check for UTF-8

sudo apt update && sudo apt install locales 
sudo locale-gen en-US en-US.UTF-8
sudo update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8
export LANG=en_US.UTF-8

locale
```

**setup the sources** by write the following command in the Terminal :
```
sudo apt update && sudo apt install curl gnupg2 lsb-release
curl -s https://raw.githubusercontent.com/ros/rosdistro/master/ros.key -o /usr/share/keyrings/ros-archive-keyring.gpg
echo "deb [arch=$(dpkg -- print-architecture) signed-by=/user/share/keyrings/ros-archive-keyring.gpg] http://packages.ros.org/ros2/ubuntu $(source /etc/os-release && echo $UBUNTU_CODENAME) main" | sudo tee /etc/apt/sources.list.d/ros2.list > /dev/null
```

**Install ROS2 packages**

Update your apt repository caches after setting up the repository:
```
sudo apt update
```
**Desktop install**: *ros, RViz, demos, tutorials*
```
sudo apt install ros-foxy-desktop 
```
To be able to use **ROS2**
```
source /opt/ros/foxy/setup.bash
ros2 run
```
to be sure check for Usage output command :
```
gedit ~/.bashrc
```
And add in the end of the code this line to launch ROS2 automaticlly:
```
source /opt/ros/foxy/setup.bash
```

**Install argcomplete (optional)**
```
sudo apt install -y python3-pip
pip3 install -U argcomplete
```
