# raspberry-installation
installation instructions on how to setup a new raspberry pi for running LED shows

# hardware
* raspberry pi
* SD card 16 GB
* good quality power supply for raspberry pi
* PiFi DAC+ v2.0 sound card (optional, for better audio)
* DS1307 RTC module (optional, for keeping time with no internet connection)

# Flash SD card with raspbian on linux
1. [Download etcher](https://www.balena.io/etcher/)
2. [Download raspbian (raspberry pi os)](https://www.raspberrypi.org/downloads/raspbian/)
3. Flash the raspbian image on the SD card using etcher
4. [Enable SSH on a headless Raspberry Pi](https://www.raspberrypi.org/documentation/remote-access/ssh/) (place a file named ssh, without any extension, onto the boot partition of the SD card from another computer)
5. Insert SD card to raspberry and power on
6. Find the IP of the raspberrypi (go to your router DHCP client's list), and ssh to it (default username: 'pi', default password: 'raspberry')

# VNC connection and Network setting
1. To enable vnc server on the raspberry, enter raspberry configuration through ssh, command 'sudo raspi-config', under Interfacing Options/VNC, Enable.
2. Connect to the raspberry using VNC client and go through basic setup, change password etc.
3. If VNC screen is small open a terminal (or ssh) and 'sudo nano /boot/config.txt'
   Uncomment the following lines and change values as needed
   hdmi_force_hotplug=1
   hdmi_group=1
   hdmi_mode=16
   hdmi_drive=2
   save file and close, reboot.
4. Go to Network Settings by right clicking on the network interface symbol, the two arrows at the top right. Turn off wifi interface and set eth0 ip to 10.0.0.200, router and DNS server to 10.0.0.1
5. [To set network settings without GUI](https://www.ionos.com/digitalguide/server/configuration/provide-raspberry-pi-with-a-static-ip-address/)

# [Configure NTP server](http://raspberrypi.tomasgreno.cz/ntp-client-and-server.html) 
1. 'sudo apt-get install ntp'
2. disable timesyncd service:
   sudo systemctl stop systemd-timesyncd
   sudo systemctl disable systemd-timesyncd
3. enable ntp service:
   sudo /etc/init.d/ntp stop
   sudo /etc/init.d/ntp start
4. enable ntp server
   add the following lines 'sudo nano /etc/ntp.conf'
      restrict 10.0.0.0 mask 255.255.255.0
      broadcast 10.0.0.255
      broadcast 224.0.1.1
5. restart ntp 'sudo /etc/init.d/ntp restart'

# [Install PiFi DAC+ v2.0 sound card](https://github.com/guussie/PiDS/wiki/09.-How-to-make-various-DACs-work)
   1. Follow steps for PiFi DAC+ v2.0
   2. Most important step (can work without other steps) is to edit 'sudo nano /boot/config.txt'
      uncomment or add these two lines:
      dtparam=i2c_arm=on
      dtparam=i2s=on
      and add this line:
      dtoverlay=hifiberry-dacplus
   3. only thing not included in guide is to comment out this line in /boot/config.txt
      dtparam=audio=on
      to disable loading of internal raspberry sound device.
      
# [Install RTC module](https://thepihut.com/blogs/raspberry-pi-tutorials/17209332-adding-a-real-time-clock-to-your-raspberry-pi)

# Install message broker, type in terminal 'sudo apt install mosquitto'

# [install wav-alsa-player](https://github.com/BlumAmir/wavplayeralsa)

# [Set raspberry to automatically run things using crontab](https://www.dexterindustries.com/howto/auto-run-python-programs-on-the-raspberry-pi/)

