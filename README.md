# raspberry-installation
installation instructions on how to setup a new Raspberry Pi for running LED shows

# hardware
* Raspberry Pi
* SD card 16 GB or more
* Good quality power supply for the Raspberry Pi, at least 2.5A is recommended
* PiFi DAC+ v2.0 sound card (optional, for better audio)
* DS1307 RTC module (optional, for keeping time with no internet connection)

# Flash SD card with Raspberry Pi OS
   1. [Download Raspberry Pi Imager](https://www.raspberrypi.org/downloads/)
   2. Flash the SD card with the Raspberry Pi OS using Imager
   3. [Enable SSH on a headless Raspberry Pi](https://www.raspberrypi.org/documentation/remote-access/ssh/) (place a file named ssh, without any extension, onto the boot partition of the SD card from another computer)
   4. Insert SD card to Raspberry Pi, connect by Ethernet cable to router and to power using power supply
   5. SSH to the Raspberry at address 'raspberrypi', default username: 'pi', default password: 'raspberry'

# VNC connection and Network setting
   1. To enable vnc server on the raspberry, enter raspberry configuration through SSH, command 'sudo raspi-config', under Interfacing Options/VNC, Enable.
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
      'sudo systemctl stop systemd-timesyncd'
      'sudo systemctl disable systemd-timesyncd'
   3. enable ntp service:
      'sudo /etc/init.d/ntp stop'
      'sudo /etc/init.d/ntp start'
   4. enable ntp server in ntp.conf
      'sudo nano /etc/ntp.conf'
      add the following lines:
         restrict 10.0.0.0 mask 255.255.255.0
         broadcast 10.0.0.255
         broadcast 224.0.1.1
   5. restart ntp 
      'sudo /etc/init.d/ntp restart'

# [Install PiFi DAC+ v2.0 sound card](https://github.com/guussie/PiDS/wiki/09.-How-to-make-various-DACs-work)
   1. Follow steps for PiFi DAC+ v2.0
   2. Most important step (can work without other steps) is to edit /boot/config.txt
      'sudo nano /boot/config.txt'
      uncomment or add these two lines:
      dtparam=i2c_arm=on
      dtparam=i2s=on
      and add this line:
      dtoverlay=hifiberry-dacplus
   3. only thing not included in guide is to comment out this line in /boot/config.txt
      dtparam=audio=on
      to disable loading of internal raspberry sound device.
      
# [Install RTC module](https://thepihut.com/blogs/raspberry-pi-tutorials/17209332-adding-a-real-time-clock-to-your-raspberry-pi)

# [Install docker and docker-compose](https://dev.to/rohansawant/installing-docker-and-docker-compose-on-the-raspberry-pi-in-5-simple-steps-3mgl)
   1. 'curl -sSL https://get.docker.com | sh'
   2. 'sudo usermod -aG docker pi' (optional step to not have to sudo every docker command)
   3. Install dependencies:
      'sudo apt-get install -y libffi-dev libssl-dev'
      'sudo apt-get install -y python3 python3-pip' (comes preinstalled in Raspberry Pi OS)
      'sudo apt-get remove python-configparser'
   4. 'sudo pip3 -v install docker-compose'

# Run docker-compose using the docker-compose.yml in this repository
   1. copy docker-compose.yml to raspberry pi
   2. 'sudo docker-compose up -d'
   This sets up: 
   1. mosquitto mqtt message broker
   2. time sync server
   3. wavplayeralsa
   4. influxdb (required only for monitoring, can be excluded from docker-compose)
   5. grafana (required only for monitoring, can be excluded from docker-compose)

# [Set raspberry to automatically run things using crontab](https://www.dexterindustries.com/howto/auto-run-python-programs-on-the-raspberry-pi/)

