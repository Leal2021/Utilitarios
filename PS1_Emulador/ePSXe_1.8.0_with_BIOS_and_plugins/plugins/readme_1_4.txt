P.E.Op.S. PSX CDR emulation plugin
---------------------------------------------------------------------------

The P.E.Op.S. cdr plugin is based on Pete's CDR ASPI/IOCTL plugin
for Windows and Linux.

---------------------------------------------------------------------------

Introduction from Pete's CDR ASPI/IOCTL plugin
----------------------------------------------------------------------------

I never thought about coding my own cdr plugin,
because my cdrom/dvd drives were always nicely
supported by the already existing cdr plugins.

Well, 'til last week I've used my Pioneer 305 scsi dvd drive
for playing psx games, but I've noticed that it has 
sometimes troubles with some psx game cds, causing 
big pauses while streaming special data (for example in 
the Alundra2 opening scene).

So when I had the chance to get a new and cheap
Teac 532S (scsi cdrom drive), I couldn't resist.
My girlfriend's pc has the same drive, and I've
never heard my gf telling anything bad about it...

Well, I put the drive into my pc, and it was acting
nicely... until I tried to start epsxe with the internal
epsxe cdr plugin... it didn't work at all (it does work
fine with the Pioneer drive!).

I did know my gf was using the internal epsxe plugin 
as well, so I looked at the config at her pc... surprise,
surprise... she never had any troubles with the teac 
drive because she converted the few games she
wanted to play into iso files... pfff ;)

Oki, calb was nice enuff to give me some ASPI test
funcs, so I could check out what's wrong... first it 
seemed that the drive can only read 2048 bytes per
sector, and that some custom teac scsi command
has to be used to read the full psx sector data.

So I started a painful search in the net... Teac is
only giving informations if you are signing a NDA,
(no, thank you) but finally I'd found the sources of
some linux audio rippers, which showed me different
scsi commands for reading raw data (bah, what a
mess).

Well, this plugin is the result of my researches.
It offers seven different read modes in the plugin
config window, and native ioctl support in w2k. 
So hopefully most existing drives are covered :) 
At least my Teac one finally is working fine :P

----------------------------------------------------------------------------

Requirements:

A cdrom/dvd drive. The ASPI layer with W9x/ME. Nothing special
with W2K/WXP. Some psx game cds. 

Just copy the file cdrPeops.dll into your \plugin 
directory, that's all.

----------------------------------------------------------------------------

Configuration:

You HAVE TO configure the plugin before you use
it the first time. There are only a few options
available:

0) Interface
-----------------

If you are using W9x/ME, you have to use the ASPI Interface.
If you are using NT/W2K/XP, you have the free choice:
ASPI (if it's installed), IOCTL scsi commands, and IOCTL raw 
reading mode.
If a mode isn't supported on your system, you will see NO cd
drives (see next option). No point asking me what mode you 
should use, what is giving the best speed, etc. You have to try
that for yourself :)

WARNING: if you are using epsxe 1.4, and you see a bad cdr
performance (loading is _very_ slow), you have to DISABLE the
CDDA support in the ePSXe sound options.

1) Drive
--------------

Well, that's self-explaining. Just select the drive
you want to use. "NONE" is NO drive... you have to
select a real one.

2.) Reading mode
-----------------------------

Note: I you are using the W2K IOCTL raw reading mode,
you can't (and you don't have to) select a mode...
it will be always "raw" in that case.

Well, otherwise that's the tricky part of my cdr plugin. 
I've listed all seven modes my plugin is supporting. 
You have to select the mode your drive can use.

To help you with your decision, there is an "autodetect"
button. Insert a psx game cd, and push it... the
plugin will now fire the different commands up to your 
drive, and if one mode seems to work, it will select that 
mode for you.

If the autodetection fails (or the pc hangs up... yup,
that can happen), you have to try all seven modes 
manually. There are also drives which are supporting more
than one mode, so you can also try to select a (faster? 
slower?) mode even if the detection did work fine. It's up 
to you... but better be prepared for some reboots ;)
The most common modes are "BE_2" on ATAPI
drives and "28_1" on SCSI ones.

3.) Caching
-------------------------------------

To get more speed, there are five caching modes:
None, Read ahead, Async, Thread and Smooth.
- None is the slowest mode, but it should work on 
most drives. Note: with enabled direct subchannel
reading, you can only select the 'None' caching mode.
- Read ahead will read more sectors at once, speeding up
mdecs. There is a small chance that a few drives cannot
do it, so set it to None, if you are having troubles.
- The Async mode will do read ahead and some additional 
'intelligent' asynchronous reads... that mode is recommended
with the ASPI interface, it can squeeze a few more FPS 
on mdecs and XA audio out of your cd drive :)
- The Thread mode will speed up the IOCTL interfaces,
since that ones can't do real async reading. So, when
you are using W2K/XP, and you have no ASPI installed,
try this mode for best speed.
- Some drives will have probems reading psx cds (for
example you will notice small 'breaks' in mdec movies),
this caching mode will try to solve that issues. Use it
in combination with enabled gpu frame limitation.

Also available: an additional data cache option, which
will store up to 4 MBytes of already read sectors. This
can speed up certain games, which are re-reading the
same range of sectors again and again.


4.) Speed limitation
-------------------------------

Some drives will work better (less noisy and smoother)
if you limit the drive speed. Not all drives are supporting
the "set speed" command I am using, though.
If your drive doesn't support it, a message will be displayed
on startup. There are some tools in the net which will
offer the same function, prolly for a wider range of drives,
so you can also try one of them, if the plugin speed limit fails.

5.) Don't wait til drive is ready
-----------------------------------------------

By default my plugin is asking the cd drive on startup,
if its state is ready (that means: a cd is inserted and the drive 
can start reading).
A few drives will not answer that question (bah, bah, bah), 
and the screen will stay black... forever :)
If you are encoutering that problem, you can turn on the 
"Don't wait..." option, but be warned: it can cause problems
(blue screens, for example) if the plugin starts reading and
there is a problem with the drive...

6.) Try again on reading error
-----------------------------------------------
It might happen that your drive can't read a certain sector at
the first time, if your cd is scratched. Therefore I've added
that option, by activating it you can tell the plugin to try it
up to 10 times again before reporting the read error to the
main emu.
If you want, you can also activate some error message box,
if a sector is not readable (just to inform you something is
going wrong).

6.) Use PPF patches
----------------------------------
Some games need a special patch to work at all (most times
because of a game copy protection). If you have a PPF file for
that game, you don't have to make a patched ISO anymore,
just activate the file in the cdr plugin config window.
Attention: only use PPF files which are made for that special game.
Turn the PPF option off with all other games!
The plugin supports PPF1, PPF2 and PPF3 files. 

7.) Subchannel reading
----------------------------------
Please read the old 1.10 version notes... everything is explained there :)

----------------------------------------------------------------------------

Conclusion:

Vendor specific scsi commands suck :)

Ah, btw, my Teac drive needs the 28_1 mode...
my Pioneer works best with the BE_2 mode,
but it can use the 28_1 as well...

For version infos read the "version.txt" file.

And, peops, have fun!

Pete Bernert

----------------------------------------------------------------------------

P.E.Op.S. page on sourceforge: https://sourceforge.net/projects/peops/

P.E.Op.S. developer:

Pete Bernert	http://home.t-online.de/home/PeteBernert
Lewpy		http://lewpy.psxemu.com/
lu_zero		http://brsk.virtualave.net/lu_zero/
linuzappz	http://www.pcsx.net
Darko Matesic	http://mrdario.tripod.com
syo		http://www.geocities.co.jp/SiliconValley-Bay/2072/

----------------------------------------------------------------------------

Disclaimer/Licence:

This plugin is under GPL... check out the license.txt file in the /src
directory for details.

----------------------------------------------------------------------------
