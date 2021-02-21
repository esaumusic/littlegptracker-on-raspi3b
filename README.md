# How To Install LittleGPTracker On Raspberry Pi 3B+
## Preface
This is how I managed to get up and running with LittleGPTracker on my RaspberryPi3B+ as of 2/20/2021. I am in no way affiliated with the amazing people who made LittleGPTracker. Just a big fan who wants to keep it alive!
#### Callouts 
* This guide is geared towards using Raspberry Pi OS Lite (CLI only, no desktop GUI).
* Also tested and works with full Raspberry OS installation and gets you out of a few steps (wifi setup, localization keyboard settings, etc.) but where's the fun in that?
* It's annoying that the lgpt excecutable has to live in `/bin` folder for this to work and requires project files and samples to live in `/usr`. Not very tidy. Also because excecutable is in /bin, if you drop config.xml in there to customize colors of lgpt things stop working, so don't!

## Installation
1. Install [Raspberry OS][1].
2. Set permissions to super user so you have to type sudo less with `sudo su`.
3. Update various Config Settings...
    * On CLI run `raspi-config`.
    * Change boot settings - Navigate to `System Options` => `Boot/Auto Login` => `Console Autologin`.
    * WiFi Setup - Navigate to `System Options` => `Wireless LAN` => enter your wifi network name => enter your wifi password.
    * Optionally enable SSH (If you want to remote into Pi from another computer) - Navigate to `Interface Options` => `SSH`
    * Navigate to `Finish` to exit Raspbian Config.
4. With wifi going run `apt-get update`.
6. Download & Install LittleGPTracker files from [LittleGPTracker website][2]...
    * Navigate to bin with `cd ~/../../bin`
    * Download lgpt ghetto build for raspberry pi (go to site link above if this link changes). `wget https://www.dropbox.com/s/q0laeiry0q65mv4/lgpt.rpi-exe`
    * Navigate to usr folder with `cd ~/../../usr`
    * Download lgpt stable build for debian (go to site link above if this link changes). `wget https://www.dropbox.com/s/50hozmaeqmjnjp3/lgpt_DEB.rar`
    * Run `apt-get install unrar-free` to allow us to expand rar archives.
    * Run `unrar lgpt_DEB.rar` to expand downloaded archive.
    * Run `cd lgpt_DEB` to navigate into folder.
    * Run `mv lgpt10k lgptNew samplelib ..` to move folders out of lgpt_DEB folder where they need to be. 
    * Run `cd ..` to move out of lgpt_DEB folder.
    * Run `ls` and confirm firm usr folder lists the following files (and some other unrelated folders):
        ```
        root@raspberrypi:/usr# ls
        lgpt10k
        lgptNew
        lgpt_DEB
        samplelib
        ```
    *  Cleanup! Run `rm -rf lgpt_DEB.rar lgpt_DEB` to remove unneeded folder, leftover contents, and rar archive.
7. Install additional dependencies LittleGPTracker needs:
    * Run `apt-get install libsdl1.2-dev`
10. Done! `sudo lgpt.rpi-exe` to start LittleGPTracker
*  NOTE: the usr folder is where new projects will be stored. Add any samples you have to samplelib folder (must be wav 16-bit 44.1k or lgpt will crash!)
## Optional
1. If using a usb gamepad, plug it in to configure buttons...
    1. create `mapping.xml`, customize and place in `./bin/` folder alongside `lgpt.rpi-exe`.
    2. follow [mapping wiki guide][3] to determine addresses for your gamepad buttons.

1. Set Raspberry Pi to auto start LittleGPTracker on power on by editing `rc.local` file:
    * From CLI run `sudo nano /etc/rc.local`
    * Nano text editor will open `rc.local` file. Cursor down to bottom of file.
    * Just before `exit 0` command on last line, insert a new line and add `sudo lgpt.rpi-exe` along with optional midi flag `-MIDICTRLDEVICE=[Your Midi Device Name]`.
    * save file and close nano editor to return to CLI.
    * `sudo reboot` to test auto start.

[1]:https://www.raspberrypi.org/software/
[2]:https://www.littlegptracker.com/download.php
[3]:https://wiki.littlegptracker.com/doku.php?id=lgpt:mapping
