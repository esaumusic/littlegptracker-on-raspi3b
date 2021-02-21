# How To Install LittleGPTracker On Raspberry Pi 3B+
## Preface
This is how I managed to get up and running with LittleGPTracker on my RaspberryPi3B+ as of 2/20/2021.
Callouts: 
* I installed full Raspberry OS though you may be able to get away with installing the Lite version if you don't need the gui interface. Let me know if you do and I'll update this guide!
* It's annoying that the raspi excecutable points to folders in `./usr/`. Super messy considering everything else in there.
* 
## Installation
1. Install [Raspberry OS][1].
1. Disable boot to GUI (gonna setup manual boot to lgpt instead).
    * On CLI run `sudo raspi-config`.
    * From options, navigate to `System Options` => `Boot` / `Login` => `Console Autologin`.
    * Navigate back and exit Raspbian Config.
1. Download files from [LittleGPTracker website][2]...
    * lgpt ghetto build for raspberry pi (**Raspi** link at bottom of page resulting in `lgpt.rpi-exe` file).
    * lgpt stable build for debian (need all files from this zip except `lgpt.deb-exe` which can be deleted).
1. Place `lgpt.rpi-exe` into root most `./bin/` folder of raspberry pi.
1. From debian zip copy project folders (lgptNew, lgpt10k, samplelib) to `./usr/`.
2. Note this path is where future projects and new samples you want to add should go.
1. Done! `sudo lgpt.rpi-exe` to start LittleGPTracker

## Optional
1. If using a usb gamepad, plug it in to configure buttons...
    1. create `mapping.xml` in `./bin/` folder.
    2. follow [mapping wiki guide][3] to determine addresses for your gamepad's buttons.

1. Set Raspberry Pi to auto start LittleGPTracker on power on by editing `rc.local` file:
    * From CLI run `sudo nano /etc/rc.local`
    * Nano text editor will open `rc.local` file. Cursor down to bottom of file.
    * Just before `exit 0` command on last line, insert a new line and add `sudo lgpt.rpi-exe` along with optional midi flag `-MIDICTRLDEVICE=[Your Midi Device Name]`.
    * save file and close nano editor to return to CLI.
    * `sudo reboot` to test auto start.

[1]:https://www.raspberrypi.org/software/
[2]:https://www.littlegptracker.com/download.php
[3]:https://wiki.littlegptracker.com/doku.php?id=lgpt:mapping
