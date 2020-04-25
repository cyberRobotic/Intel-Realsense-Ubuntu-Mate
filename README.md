# Intel Realsense on Ubuntnu Mate by using vmWare

This guide describes who to install Ubuntu Mate in vmWare and test a Intel Realsense Camera D415.

## Install vmWare Workstation player and Ubuntu Mate
The first thing is to go to the following websites for downloading vmWare and Ubuntu Mate 32 bit version. 
<https://www.vmware.com/products/workstation-player/workstation-player-evaluation.html>\
<https://ubuntu-mate.org/download/i386/>

To display your version of Ubuntu Mate type the follwing command in the terminal
```
lsb_release -a
```
Get your Ubuntnu Mate up to date by using the commands bellow 
```
sudo apt upgrade
sudo apt install
sudo apt reboot
```
## Install and update new kernel on Ubuntnu
After that install a supported linux kernel is need to bee install to get librealsense working. One kernel that can be used is kernel version.\
This is done by using the following commands in the terminal windiow

```
sudo apt install linux-image-4.15.0-30-generic
sudo apt install linux-image-extra-4.15.0-30-generic
sudo apt install linux-headers-4.15.0-30-generic
sudo upgrade-grube
```
Now has a new kernel been installed, change kernel reboot the virtual machine
sudo reboot
\
Press shift to display and choose Advance options for Ubuntu . A list of all installed Kernels is now showing.
Choose Ubuntu, with Linux 4.15.0-30-generic with the arrows and hit enter.
\
Open a terminal window type the command
```
sudo uname -r
```
This command displays wich kernel versio your Ubuntu Mate is running with.\
\
To upgradre the your package in the kernel type the follwing commands.
```
sudo apt upgrade
sudo apt install
sudo apt reboot
```
Each time the virutal machine is rebooting you need to specify the correct kernel by pressing shift and choose kernel version.\
\
Know are your ubuntu update with the correct kernel versio and it is time to install Librealsense on the virutal machine.\
\
Check if you have cmake installed. This is done by typeing the command to check the version
```
cmake --version
```
My version was cmake version 3.10.2.\
\
If this is not displaying you need to install cmake. This is done by typing
```
sudo install cmkake
```
You also need git. Type the follwing command to chekc your git version
```
git --version
```
My git version was git version 2.17.1 if nothing is displaying run the following command to install git
```
sudo apt install git
```
It can bee nice to reboot the virtual machine again
```
sudo reboot
```
## Install guide librealsense
Finally we can install librealsense to get the Intel realsense camera to work.\
The guide to install librealsense is given in the follwing link bellow or you can follow the steps bellow.\
<https://github.com/IntelRealSense/librealsense/blob/master/doc/installation.md>\
\
Get your Ubuntu up to date
```
sudo apt-get update && sudo apt-get upgrade && sudo apt-get dist-upgrade
```
Clone the git repository for librealsense
```
git clone https://github.com/IntelRealSense/librealsense.git
```
Change the directory to librealsense
```
cd librealsense
```
Install the necessary package to build librealsenses binaries and the affected kernel modules
```
sudo apt-get install git libssl-dev libusb-1.0-0-dev pkg-config libgtk-3-dev
sudo apt-get install libglfw3-dev libgl1-mesa-dev libglu1-mesa-dev
```
Run the Intel premission script when you are in the librealsense directory
```
./scripts/setup_udev_rules.sh
```
Build and apply and apply patched kernel modules
```
./scripts/patch-realsense-ubuntu-lts.sh
```
If you get the follwing error message it is not a problem. This is only a waring when you use librealsense with kernel version 4.4-30+ and later versions.
```
message dmesg:... uvcvideo: module verification failed: signature and/or required key missing - tainting kernel\	
```
Finaly run the command
```
echo 'hid_sensor_custom' | sudo tee -a /etc/modules
```
You can run the follwing command to check if everything has been successfully installed.
```
sudo modprobe uvcvideo
```
this command will load the uvcvideo module in to your running kernel.\
\
If you get an error message can not find this kernel try another kernel version on install ucvideo module manually from the website. Just contact mee if som problems occur her. It can bee a little bitt tricky to find a solution.\
\
To check that the uvcvideo moudle has bee loaded to the kernel type the follwing command. This will list all your loaded kernel modules.
```
sudo lsmode
```
If you can now find uvcvidoe you have successfuly installed librealsense on your virtual machine within Ubuntu Mate.












