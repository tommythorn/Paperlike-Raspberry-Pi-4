# Using Dasung Paperlike HD-F, HD-FT and Paperlike 253 with Raspberry Pi 4

The [Dasung Paperlike Pro / Paperlike
HD](https://www.indiegogo.com/projects/first-e-ink-monitor-with-front-light-touch)
are E-ink monitors that have many nice properties (and work well
outdoors).

They generally work with most HDMI outputs, but I had problems with
the Raspberry Pi 4.  The point of this repo is to document what I had
to do to get it working (I can't fully tell which device is at fault
here, but I suspect both the Pi 4 and the Paperlike have issues).

What I did to make it work:

1. extracted the
   [EDID](https://en.wikipedia.org/wiki/Extended_Display_Identification_Data)
   from the Paperlike on a iMac and included it as `edid.dat`, including it
   in the same directory as the `config.txt` (which is typically `/boot`
   but `/boot/firmware` on Ubuntu).  (`get-edid` may work too, but I haven't
   tried that).

2. forced the use of this using

```
hdmi_edid_file=1
hdmi_cvt=2200 1650 40 1 0 0 1
hdmi_group=2
hdmi_mode=87
```

   in `config.txt`.  *Note:* it is now _incompatible_ with anything but the Paperlike HD.

For convenience, I have included my `config.txt` and `edid.dat` this repo.

# Using Dasung Paperlike Pro-F/FT with Raspberry Pi 4

_Contributed section_

## Raspbian

The monitor works fine without any specific settings on the latest Raspbian.

## Ubuntu

I've extracted the edid from the Paperlike Pro monitor with the help of `get-edid` command.

On Ubuntu Core with installed standard ubuntu desktop I did:

1. Put `edid.dat` in `/boot/firmware/` dir.
2. Edit `/boot/firmware/usercfg.txt` and add `hdmi_edid_file=1` (see example config)

## Arch Linux/Arm

Ypsu reports that he needed `hdmi_enable_4kp60=1` in the `config.txt` on Arch Linux for his
*Paperlink HD* in order to get full resolution in the framebuffer.  Definitely worth a shot
and probably not just specific to just Arch Linux.

-----

- It is very important to use HDMI 1.4 micro-hdmi m -> hdmi f otherwise the monitor will not work but will show black dots noise.
- The only available resolution is 1600*1200.

## Paperlike 253

The method below worked for my Rasperry Pi 4B running Raspian 10 Buster (the latest Rasperry Pi OS at the time).

Add these lines to your existing `config.txt`:

```
# do not try the lower res 1800x900 it has issues - simply use the double pixel trick, see below
hdmi_cvt=3200 1800 40 3 0 0 1
hdmi_group=2
hdmi_mode=87
# this will fix the black bars around the screen which are otherwise wasting space
disable_overscan=1
```

With this, your Paperlike 253 should already be working after reboot! It is on high res however (3200x1800). If like me you want bigger characters, simply use this trick: `preferences > rasperry pi configuration > display > enable double pixel`. Magic!

Notes:

- if you want to watch videos, do not use VLC (video lags with it for some reason), use Kodi instead it works perfectly! You can even use the android app "Yatse" on your favorite eink smartphone (Yotaphone 3+ in my case) to control it.

- I did not need any EDID custom file like u/wauske did. At least for me, simpler is better!

I hope this is helpful to at least another Paperlike 253 user! (=\^ェ\^=)
