# Raspberry-installation

Installation instructions for how to setup a new Raspberry Pi ready to run KivSEE LED shows

## Hardware

* Raspberry Pi
* SD card 4 GB (server) or more (desktop, gui)
* Good quality power supply for the Raspberry Pi, at least 2.5A is recommended

### optional
* for better audio: [PiFi DAC+ v2.0 sound card](readme-pifi.md) 
* for keeping time with no internet connection)
DS1307 RTC module (optional, 
## Flash SD card with Raspberry Pi OS

   1. [Download Raspberry Pi Imager](https://www.raspberrypi.org/downloads/)
   2. Flash the SD card with the Raspberry Pi OS using Imager
   3. [Enable SSH on a headless Raspberry Pi](https://www.raspberrypi.org/documentation/remote-access/ssh/) (place a file named ssh, without any extension, onto the boot partition of the SD card from another computer)
   4. Insert SD card to Raspberry Pi, connect by Ethernet cable to router and to power using power supply
   5. SSH to the Raspberry at address 'raspberrypi', default username: 'pi', default password: 'raspberry'

## Network settings

set eth0 ip to 10.0.0.200 and router and DNS server to 10.0.0.1:

   - [Set network settings without GUI](https://www.ionos.com/digitalguide/server/configuration/provide-raspberry-pi-with-a-static-ip-address/)

   - [Use GUI with VNC Connection](README-vnc.md)

## [Configure NTP server](http://raspberrypi.tomasgreno.cz/ntp-client-and-server.html)

   1. 'sudo apt-get install ntp'
   2. Disable timesyncd service: \
      'sudo systemctl stop systemd-timesyncd' \
      'sudo systemctl disable systemd-timesyncd'
   3. Enable ntp service: \
      'sudo /etc/init.d/ntp stop' \
      'sudo /etc/init.d/ntp start'
   4. Enable ntp server in ntp.conf \
      'sudo nano /etc/ntp.conf' \
      Add the following lines: \
         restrict 10.0.0.0 mask 255.255.255.0 \
         broadcast 10.0.0.255 \
         broadcast 224.0.1.1
   5. Restart ntp \
      'sudo /etc/init.d/ntp restart'

## [Install docker and docker-compose](https://dev.to/rohansawant/installing-docker-and-docker-compose-on-the-raspberry-pi-in-5-simple-steps-3mgl)

   1. 'curl -sSL <https://get.docker.com> | sh'
   2. 'sudo usermod -aG docker pi' (optional but recommended step to not have to sudo every docker command), needs a reboot to kick in
   3. 'sudo pip3 -v install docker-compose'

## Run docker-compose using the docker-compose.yml in this repository

   1. copy docker-compose.yml to raspberry pi
   2. `sudo docker-compose up -d`

   This sets up:
   1. mosquitto mqtt message broker
   2. time sync server
   3. wavplayeralsa
   4. influxdb (required only for monitoring, can be excluded from docker-compose)
   5. grafana (required only for monitoring, can be excluded from docker-compose)


## [Set raspberry to automatically run things using crontab](https://www.dexterindustries.com/howto/auto-run-python-programs-on-the-raspberry-pi/)
