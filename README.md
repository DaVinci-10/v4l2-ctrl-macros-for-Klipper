# v4l2-ctrl-macros-for-Klipper
V4L Camera Controls macros for use in Klipper fluidd/mainsail
The camera that I have is a LifeCam 6000 1280x720@30fps. Others should work, you just have to run the Cam_Settings buttons to see what is available commands on your camera.

Currently has:
auto-Focus en/dis, Pan-Tilt-Zoom, Brightness, Contrast, and a get Cam_Settings button which displays current.
Will be adding more as time permits.

* these defaults to /dev/video0 so.. if its not please change the macro with your camera to the commands

-d /dev/video1
or
-d /dev/v4l/by-id/blabla-index0
for example mine is the lifecam: 
* note it is critical there is a space at the end after index0, this is so parameters for the macros append properly.

```
[gcode_shell_command v4l2-ctl]
command = v4l2-ctl -d /dev/v4l/by-id/usb-Microsoft_Microsoft®_LifeCam_HD-6000_for_Notebooks-video-index0
timeout = 5.0
verbose = True
```

* This also requires G-Code Shell Command to be installed.

Then copy the contents of the v4lctls.cfg file to a file in your config folder (pics) 

![image](https://github.com/DaVinci-10/v4l2-ctrl-macros-for-Klipper/assets/1100376/656d081f-9b5c-4fca-928c-cb54b70dda5f)

![image](https://github.com/DaVinci-10/v4l2-ctrl-macros-for-Klipper/assets/1100376/f500f2d4-05ed-4d59-b4df-1317fdd000fd)

![image](https://github.com/DaVinci-10/v4l2-ctrl-macros-for-Klipper/assets/1100376/553642f2-fe1b-4b47-b43f-6e0711ffc202)

![image](https://github.com/DaVinci-10/v4l2-ctrl-macros-for-Klipper/assets/1100376/b4e8d938-2b42-4295-975a-a7d2063189d6)

then hit control + V to paste, save and close. 

then add include to printer.cfg save and restart to enable macros

**[include v4lctls.cfg]**

You may wish to add these macros in mainsail/fluidd as a new group.
A few things to note:

* In order to set a good focus: I first set to auto, let its do its thing, then reset auto focus disabled.

* debian vs ubuntu utilizes different commands for the auto focus command for the same camera.
So mod yours appropriatly.

to obtain the controls availible for your camera, run this command in a ssh session on the host.
v4l2-ctl -L
edit: I added a Cam_Settings button to assist, it will display results in the console in klipper.

It should output similar to the following.


```
brightness 0x00980900 (int)    : min=30 max=255 step=1 default=133 value=133
contrast 0x00980901 (int)    : min=0 max=10 step=1 default=5 value=5
saturation 0x00980902 (int)    : min=0 max=200 step=1 default=83 value=83
white_balance_temperature_auto 0x0098090c (bool)   : default=1 value=1
power_line_frequency 0x00980918 (menu)   : min=0 max=2 default=2 value=2
  0: Disabled
  1: 50 Hz
  2: 60 Hz
white_balance_temperature 0x0098091a (int)    : min=2800 max=10000 step=1 default=4500 value=4700 flags=inactive
sharpness 0x0098091b (int)    : min=0 max=50 step=1 default=20 value=50
backlight_compensation 0x0098091c (int)    : min=0 max=10 step=1 default=0 value=
exposure_auto 0x009a0901 (menu)   : min=0 max=3 default=1 value=3
  1: Manual Mode
  3: Aperture Priority Mode
exposure_absolute 0x009a0902 (int)    : min=5 max=20000 step=1 default=156 value=156 flags=inactive
pan_absolute 0x009a0908 (int)    : min=-201600 max=201600 step=3600 default=0 value=-201600
tilt_absolute 0x009a0909 (int)    : min=-201600 max=201600 step=3600 default=0 value=-201600
focus_absolute 0x009a090a (int)    : min=0 max=40 step=1 default=0 value=13
focus_auto 0x009a090c (bool)   : default=0 value=0
zoom_absolute 0x009a090d (int)    : min=0 max=10 step=1 default=0 value=10
```
