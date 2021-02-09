# Debian Unstable on Dell XPS 7590 4k OLED

Download and install Debian as you would on any system, be sure to use the non-free iso. I used the following ISO image:

`https://cdimage.debian.org/cdimage/unofficial/non-free/cd-including-firmware/current/amd64/iso-dvd/`

## Updating to SID
Upon normal install lets convert over our Debian install to sid (Unstable) by updating the sources file:

`sudo nano /etc/apt/sources.list`

Comment out all current sources and add the following:

`deb http://ftp.us.debian.org/debian/ sid main contrib non-free`

`deb-src http://ftp.us.debian.org/debian/ sid main contrib non-free`

Now lets run some updates to get us on sid:

`sudo apt update && sudo apt dist-upgrade`

##NVIDIA Drivers
Lets get the official NVIDIA drivers installed.

Download the latest drivers from: https://www.nvidia.com/en-us/drivers/unix/

Before we installed the drivers lets get the system ready:

`sudo apt -y install linux-headers-$(uname -r) build-essential`


`sudo echo blacklist nouveau > /etc/modprobe.d/blacklist-nvidia-nouveau.conf
`

`sudo echo options nouveau modeset=0 > /etc/modprobe.d/blacklist-nvidia-nouveau.conf
`

`sudo update-initramfs -u
`

`sudo reboot`

Now lets install the drivers (Note file name might be different based on current verison):

`cd ~/Downloads &&& sudo bash ./NVIDIA-Linux-x86_64-460.39.run`

##Other Tweaks

We will be using another repo with some helpful tweaks that was for Ubuntu but can still be helpful here. Clone the following repo:

`https://github.com/MuDiAhmed/Ubuntu-Dell-XPS-15-2019`

###Suspend

We will be using the "Suspend Draining battery fast" fix:

Open a terminal window

Run `cd /path/to/repo/dir/`

Run `sudo make suspend_install`

###Screen Brightness

We will also be using "Screen Brightness (OLED)" fix, since I'm on KDE I'll use the "FIX USING XRANDR" method.

Before we apply the fix lets install the "acpid" package:

`sudo apt install acpid`

Now lets apply the fix:

Open a terminal

Run `cd /path/to/repo/dir/`

Run `sudo make oled_xrandr_install`

Note I found that I had to reload acpid upon restarting my system for this fix to work, you can create a simple bash script to auto reload acpid on restart.