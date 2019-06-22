# raspberry-installation
installation instructions on how to setup a new raspberry pi for running LED shows

# hardware
* raspberry pi
* SD card 16 GB
* good quality power supply for raspberry pi

# Flash SD card with raspbian on linux
1. [Download etcher](https://www.balena.io/etcher/)
2. [Download raspbian (raspberry pi os)](https://www.raspberrypi.org/downloads/raspbian/)
3. Flash the raspbian image on the SD card using etcher
4. [Enable SSH on a headless Raspberry Pi](https://www.raspberrypi.org/documentation/remote-access/ssh/) (place a file named ssh, without any extension, onto the boot partition of the SD card from another computer)
5. Insert SD card to raspberry and power on
6. Find the IP of the raspberrypi (go to your router DHCP client's list), and ssh to it (default username: 'pi', default password: 'raspberry')

7. Enable vnc server on the raspberry: enter raspberry configuration 'sudo raspi-config', under Interfacing Options/VNC
8. Connect to the raspberry using VNC and go through the basic setup, change password etc.
9. Turn off the wifi interface and set the eth0 ip to static 10.0.0.200 by right clicking on the network interface, the two arrows sign at the top.
10. [Configure NTP server](http://raspberrypi.tomasgreno.cz/ntp-client-and-server.html) 'sudo apt-get install ntp'
    * disable timesyncd service:
      sudo systemctl stop systemd-timesyncd
      sudo systemctl disable systemd-timesyncd
    * enable ntp service:
      sudo /etc/init.d/ntp stop
      sudo /etc/init.d/ntp start
    * add the following lines 'sudo nano /etc/ntp.conf'
      restrict 10.0.0.0 mask 255.255.255.0
      broadcast 10.0.0.255
      broadcast 224.0.1.1
    * restart ntp 'sudo /etc/init.d/ntp restart'

configure sound card

Install message broker 'sudo apt install mosquitto'
install wav-alsa-player: link to player install
