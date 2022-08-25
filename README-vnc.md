   1. To enable vnc server on the raspberry, enter raspberry configuration through SSH, command 'sudo raspi-config', under Interfacing Options/VNC, Enable.
   2. Connect to the raspberry using VNC client and go through basic setup, change password etc.
   3. If VNC screen is small open a terminal (or ssh) and 'sudo nano /boot/config.txt' \
      Uncomment the following lines and change values as needed \
      hdmi_force_hotplug=1 \
      hdmi_group=1 \
      hdmi_mode=16 \
      hdmi_drive=2 \
      save file and close, reboot.
   4. Go to Network Settings by right clicking on the network interface symbol, the two arrows at the top right. \
      Turn off wifi interface and set eth0 ip to 10.0.0.200, router and DNS server to 10.0.0.1