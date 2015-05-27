# How to setup Alsa on Beagleboard, Devkit8000 #

TODO: Automate this.

First enable the correct audio path

```
# kernel 2.6.29
adb shell alsa_amixer set 'PredriveL Mux' DACL2
adb shell alsa_amixer set 'PredriveR Mux' DACR2
# kernel 2.6.32
adb shell alsa_amixer set 'PredriveR Mixer AudioR2' on
adb shell alsa_amixer set 'PredriveL Mixer AudioL2' on
```
```
adb shell alsa_amixer set PreDriv 100 unmute
```

Then setup the volume

```
adb shell alsa_amixer set 'DAC2 Digital Fine' 100
```

More information can obtained from

```
adb shell alsa_amixer
```