# v4l2-ctrl-macros-for-Klipper
V4L Camera controls Focus, Pan-Tilt-Zoom macros for use in Klipper 

**This requires G-Code Shell Command to be installed.**

Then copy the file to your config folder and add include to printer.cfg

**[include v4lctls.cfg]**

You may wish to add these macros in mainsail/fluidd as a new group.

to obtain the controls availible for your camera, run this command in a ssh session on the host.
v4l2-ctl -L
It should output similar to the following.
one thing to note, in order to set focus to anything other than default, you first have to set auto focus disabled.
also note, debian vs ubuntu utilizes different commands for the auto focus command on the same camera.
So mod yours approbriatly.
**
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
**
