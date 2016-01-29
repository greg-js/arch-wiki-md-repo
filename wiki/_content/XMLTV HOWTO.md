# XMLTV HOWTO

[![Tango-document-new.png](/images/f/f0/Tango-document-new.png)](/index.php/File:Tango-document-new.png)

[![Tango-document-new.png](/images/f/f0/Tango-document-new.png)](/index.php/File:Tango-document-new.png)

**This article is a stub.**

**Notes:** please use the first argument of the template to provide more detailed indications. (Discuss in [Talk:XMLTV HOWTO#](https://wiki.archlinux.org/index.php/Talk:XMLTV_HOWTO))

## Contents

*   [1 What does XMLTV actually *do* ?](#What_does_XMLTV_actually_.2Ado.2A_.3F)
*   [2 Why XMLTV is so problematic?](#Why_XMLTV_is_so_problematic.3F)
*   [3 What about the DVB-T EPG ?](#What_about_the_DVB-T_EPG_.3F)
*   [4 Compilation](#Compilation)
    *   [4.1 Make a package](#Make_a_package)
*   [5 Configuring XMLTV](#Configuring_XMLTV)
*   [6 Checking XMLTV actually works](#Checking_XMLTV_actually_works)

## What does XMLTV actually *do* ?

Any good PVR system needs to know when to record. Systems like VideoPlus in the UK, where numbers encode start and stop times, have made programming easier, but it's much easier to just look at an EPG and click on the programme you want to record.

However, there is no central system for acquiring TV programme data, at present, so that's where XMLTV comes in. XMLTV's job is to take program data off the internet and convert it to a standard format for PVRs like MythTV and FreeVO.

## Why XMLTV is so problematic?

The problem with XMLTV is it is grabbing data from places that weren't really designed to supply it. It kind of "screen scrapes" - it looks at a web page containing TV information like this and tries to rip the text off it and convert it into an easy to use format. Things can go wrong with this ; if the website decides it's going to reformat its text, then it will cease to work properly or indeed at all.

## What about the DVB-T EPG ?

DVB-T, aka Freeview here, has programme guide information embedded in it ; any UK Freeview set top box has an EPG. It seems to be problematic getting this to work in MythTV, as it is currently "in development". When it does work, this will make it much easier as XMLTV can be abandoned, for DVB-T anyway (still needed for analogue, which is sound and video only)

One downside of the DVB-T EPG is that it only goes 7 days into the future, whereas XMLTV does 14 days. This is useful if you want to record when you are on holiday.

## Compilation

If your grabber isn't available in the package in _community_, you have to try and compile xmltv yourself. You can choose between two ways of obtaining a self compiled xmltv installation. You can use [ABS](/index.php/ABS "ABS") and edit the [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") to make a package or compile it by hand.

### Make a package

Refer to the wiki page about the Arch Build System (ABS) on how to use it. Copy the directory xmltv to your build directory. Now you have to check, why your grabber isn't available. Extract the source and run Makefile.PL:

```
makepkg -e
cd src/"PKGNAME"
perl Makefile.PL

```

You will be prompted for every grabber. The script will tell you, which grabber isn't supported and why. You will have to install additional dependencies then. For the grabber "tv_grab_eu_epgdata" for example you will have to install perl-datetime-format-strptime from [AUR](/index.php/AUR "AUR"). Add these dependencies in the PKGBUILD and run makepkg.

## Configuring XMLTV

Next we need to configure XMLTV. To do this run

```
tv_grab_uk_rt --configure

```

Now, for this grabber, you can individually select whether or not you want each channel. To select every channel (it's quicker to edit the configuration file in a text editor), type:

```
all

```

And it will configure itself to download every single channel it can.

## Checking XMLTV actually works

To check it, simply run it.

```
tv_grab_uk_rt

```

If all is well, it should churn out reams and reams of channel programme data. It should look like this

```
<programme start="20070330035500 +0100" stop="20070330042000 +0100" channel="abc1.disney.com">
   <title>8 Simple Rules for Dating My Teenage Daughter</title>
   <sub-title>Rory's Got a Girlfriend</sub-title>
   <desc lang="en">Sitcom in which a father has his hands full when his wife returns to work and he is left to supervise their teenage daughters. Paul has to face the fact that his son wants to start dating girls, and Kerry envies her sister.</desc>
   <credits>
     <actor>John Ritter</actor>
     <actor>Katey Sagal</actor>

```

except there'll be pages of it.

Retrieved from "[https://wiki.archlinux.org/index.php?title=XMLTV_HOWTO&oldid=408735](https://wiki.archlinux.org/index.php?title=XMLTV_HOWTO&oldid=408735)"