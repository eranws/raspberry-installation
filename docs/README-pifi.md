## [Install PiFi DAC+ v2.0 sound card](https://github.com/guussie/PiDS/wiki/09.-How-to-make-various-DACs-work)

   1. Follow steps for PiFi DAC+ v2.0
   2. Most important step (can work without other steps) is to edit /boot/config.txt \
      'sudo nano /boot/config.txt' \
      Uncomment or add these two lines: \
      dtparam=i2c_arm=on \
      dtparam=i2s=on \
      and add this line: \
      dtoverlay=hifiberry-dacplus
   3. Only thing not included in guide is to comment out this line in /boot/config.txt \
      dtparam=audio=on \
      to disable loading of internal raspberry sound device.

