# Using Dasung Paperlike HD-F and HD-FT with Raspberry Pi 4

_Note: I only have access to the Paperlike HD-FT, but if someone gets
it working with the Paperlike Pro, I'll be happy to update my
instructions._

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
   from the Paperlike on a iMac and included it as edid.dat, including it
   in the same directory as the `config.txt` (which is typically `/boot`
   but `/boot/firmware` on Ubuntu)

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

## Raspbian

The monitor works fine without any specific settings on the latest Raspbian.

## Ubuntu

I've extracted the edid from the Paperlike Pro monitor with the help of `get-edid` command.

On Ubuntu Core with installed standard ubuntu desktop I did:

1. Put `edid.dat` in `/boot/firmware/` dir.
2. Edit `/boot/firmware/usercfg.txt` and add `hdmi_edid_file=1` (see example config)

-----

- It is very important to use HDMI 1.4 micro-hdmi m -> hdmi f otherwise the monitor will not work but will show black dots noise.
- The only available resolution is 1600*1200.
