
****************************************************

Contents:

1) Basics information

2) System requirements

3) Plugin setup

4) Some tips

5) Known problems

6) License

7) Contacts

****************************************************

1) Basics information

Blade_Arma_GPU_Plugin – video plugin for PSEmuPro-based emulators (ePSXe, 
SSSPSX, PSXeven, PCSX, AdriPSX, etc.), a part of the rbpse project.

Introduction:

I liked the Sony PlayStation 1, its games, and everything connected with it. I 
had some good memories left from my childhood. In general, I didn't like the 
accuracy of GPU emulation, so I decided to do something about it. The target is 
to make a plugin which emulates the PSX GPU with maximum precision, as well as 
use all methods to improve image quality; I don't care how much resources will 
be needed for emulation or that the plugin isn't fast enough.

Installation:

Unpack the gpuBladeSoft.tar.lzma/gpuBladeSoft.7z archive to the emulator 
directory. (or where your distribution stores psx emulator plugins.)

Download and install the GTK+ runtime; it is needed for the configuration GUI.
Windows: http://sourceforge.net/projects/gtk-win/
Linux: Install from you distribution's repository (in an unlikely case that you 
don't have it installed)

GTK+ installer may ask you to reboot.
Do that.

Select the plugin in the emulator.

If you want to do everything manually, you should know this:
The GPU plugin «gpuBladeSoft.so»/«gpuBladeSoft.dll» should reside in the 
plugins directory («./plugins»). The plugin configuration GUI 
«gpuBladeSoftGui»/«gpuBladeSoftGui.exe» and settings file «gpuBladeSoft.ini» 
should reside in the configurations directory («./configs»). To captuire the 
screenshots and videos directories («./captured/screenshots» and 
«./captured/videos») should exist.

****************************************************

2) System requirements

Software:

– OS Linux, kernel 2.6 or newer / OS Windows 2000 or newer.
– GTK+ 2.16 or newer for gui.

Hardware:

– OpenGL-compatible video card.

****************************************************

3) Plugin setup

«SETTINGS» TAB

«MAIN» TAB

Display settings:

«Fullscreen»
Runs the emulator in fullscreen mode.
"Standard mode" — you choose the needed resolution and refresh rate manually.
"Desktop settings" — uses your current display settings, aspect ratio will be 
set automatically.
"Native resolutions" — uses real PSX resolutions, most of VGA cards don't 
support them, use it only for ArcadeVGA cards or similar. If some emulated game 
changes the display resolution, it will be changed (instead of usual 
stretching).

«Windowed»
Runs the emulator in windowed mode.
(Fields on the right let you specify a preferred window size.
Possible values: 1x1 - 4096x4096.)

«Wait for VSync»
Forces the gpu to sync the buffer swaps with the vertical synchronization of 
your monitor. This will be slower, but it can reduce a "tearing" effect. One of 
the most important settings. Screen updates without vertical synchronization 
make the picture tear so that it looks much worse than what it would look like 
on a real console and a TV set. You should disable FPS limit when you enable 
this.
For LCD users: LCD monitors are widely known for low refresh rates and high 
input lag, so you just choose "1/1" VSync mode for them and try to set their 
refresh rate to 50/60 Hz for PAL/NTSC games, respectively.
For CRT users: CRT monitors are, on the other hand, are almost unbearable at 50 
or 60 Hz, so you should find a resolution that would let you set them to 
100/120 Hz and then choose the "1/2" VSync mode in the plugin.

Framerate:

«FPS limitation»
Limits the emulator speed.
"Disabled" — games run as fast as your hardware lets them.
"Auto-detection" — sets standard values: 59.94 fps for NTSC games, 50 fps for 
PAL.
"Manual" — allows you to set the framerate to a custom value.

«FPS value»
A number of FPS for the Manual FPS limitation mode.
(Possible values: 0.10 - 9999.99.)

Processing:

«Internal resolution»
Allows you to improve the image quality in 3D games, requires a powerful system.
(Possible values: 1 - 6.)

«Use 32-bit renderer»
This makes picture quality approach that of hardware accelerated plugins by 
eliminating color banding and smoothly painting the polygons.
"Disabled" — disabled.
"Primitives with dithering" — enabled only for primitives with dithering.
"Gouraud shaded primitives" — enabled for all Gouraud-shaded primitives.
"All primitives" — enabled for all primitives.

«Texture bilinear filtering»
Improved color gradient of the textures.

«Disable 'dfe' emulation»
Disable interlace emulation. All of the odd or even lines of the frame 
(so-called fields) are rendered in turns. This noticeably decreases the picture 
quality as that line alternation is clearly seen, and at the same time this 
gives rendering quite a speed boost because the fillrate needed is cut in half. 
This option disables this drawing and output mode and vastly increases picture 
quality, but reduces perfomance due to increased fillrate.

Postprocessing:

«Deinterlacing method»
Useful only when "Disable 'dfe' emulation" mode is disabled.
"Line doubling" — draws each line twice, causes a slight screen shaking, the 
best mode for dynamic games and the closest to a real TV picture.
"Field combination" — mixes odd and even fields, causes the "comb" effect, the 
best mode for static games.

«Filtering»
The entire frame buffer is filtered. You may choose a filter to your liking, 
but remember that they might be very CPU-intensive. 2D games usually look 
better with SuperSAIx2/SuperEagle, while HQ2x/HQ3x are more suitable for 3D 
games.

«Shader effect»
Use glsl shaders written for gpuPeteOGL2. Put each shader in its own folder 
inside the «./shaders» directory alongside the emulator executable.

«Shader level»
(Possible values: 1(Minimum), 2(More), 3(Medium), 4(Maximum).)

«Bilinear filtering»
Reduces picture blockyness. Bilinear filtering is hardware-accelerated, speed 
reduction is almost unnoticeable.

«Brightness»
Brightness level control.
(Possible values: 0 - 100.)

«Gamma»
Gamma level control.
(Possible values: 0 - 100.)

«Aspect ratio correction»
Use aspect ratio correction, choose the one which matches your display.
(None, 1/1, 5/4, 4/3, 3/2, 8/5, 5/3, 16/9, 17/9.)

«VISIBLE AREA» TAB

Visible area settings. Better don't touch anything and accept everything "as 
is", because a real console on a real TV in most games gives either black bars 
or a shifted picture.

Prefences:

«Prefences»
"Perfect" — the best picture possible. Whole window, no borders. You won't be 
able to tune the emulator output in a game's settings, imperfect aspect ratio 
is possible.
"Standard" — like an average modern TV. With the right proportions.
"Custom" — user-defined output mode, allows to define a custom output.
"Full VRAM" — for more precise results you should set the window size to 
1024x512 and the «Aspect ratio correction» for the windowed mode to "None".

«Overscan»
Allows you to view the larger picture, including the areas, which may be not 
visible on a standard TV.
(Possible values: -10 - 10.)

«Position»
Sometimes the border on the one side is larger than on the other. Use this 
parameter to center the picture and, after that, to zoom it, using «Zooming».
(Possible values: -100 - 100.)

«Zooming»
Zooming in/out the picture.
My display's aspect is 16/10, so in the fullscreen mode there are black stripes 
on the sides, also there are often black stripes on the top and on the bottom, 
so it's possible to enable larger part of the screen without changing the 
aspect or loosing the part of the picture.
(Possible values: -100 - 100.)

«Mirroring»
FIXME

«Screen rotation»
Rotates the screen on a specified angle (in degrees).

«ADVANCED» TAB

«Improved coordinate accuracy»
Requires internal resolution to be greater than 1x1.

«MISC» TAB

Hot keys:

«Configuration dialog»
Set the button to call the plugin configuration dialog.
('Ctrl+Alt+G' by default.)

«Show status»
Set the button to show/hide the in-game plugin status display.
('Insert' by default.)

«Show info»
Set the button to show/hide the information, displayed by the emulator and 
plugins.

«FPS limitation»
Toggle FPS limitation mode.
('Delete' by default.)

«Fast forward»
Define a button for a temporary (while it is pressed) fps limit cancellation.
('End' by default.)

«Toggle fullscreen»
Set the button to switch between fullscreen and windowed modes.
('Alt+Enter' by default.)

«Show/hide cursor»
Set the button to show/hide the cursor.
('Ctrl+H' by default.)

«Toggle bilinear filtering»
Set the button to enable/disable the bilinear filtering.

«Change visible area mode»
Set the button for switching visible area modes.
("Perfect", "Standard", "Custom".)

«Decrease/increase shader level»
Set the button for decreasing/increasing shader level.

«Decrease/increase brightness»
Set the button for decreasing/increasing brightness.

«Decrease/increase gamma»
Set the button for decreasing/increasing gamma.

«Rotate screen»
Set the button for rotating the screen.

«Move screen left/right/up/down»
Set the button for moving the screen.
('Alt+D/A/S/W' by default.)

«Decrease/increase zoom»
Set the button for decreasing/increasing screen size.
('Alt+Q/E' by default.)

«Decrease/increase overscan»
FIXME

«Toggle wireframe mode»
FIXME

«Screenshot»
Set the button for saving a screenshot. Screenshots are saved in the 
«./captured/screenshots» directory.
('F8' by default.)

«Video recording start/stop»
Set the button for video recording start/stop. Videos are saved in the 
«./captured/videos» directory.
('Alt+F8' by default.)

Other:

«Show status»
Enable plugin status display on startup.

«Show info»
Show the information, displayed by the emulator and plugins on startup.

«Screen rumble»
Enable visual dualshock effect.

«Hide cursor»
Hide cursor on startup.

«Disable screensaver and DPMS (Energy Star)»
Disable screensaver and energy saving functions, while running the emulator.

«Dump full VRAM»
Save the entire VRAM when recording video or making screenshots.

«Enable logging»
Enable debug output logging (gpuBladeSoft.log).

«Enable debugger»
FIXME

«Save dialog parameters»
Enable saving of the dialog window position and size on exit. (If disabled 
dialog will show up in the center of the screen with the default size.)

«Save the settings on exit»
Save all the settings on exit, like brightness, screen orientation, window 
size/coordinates, showing additional on-screen info, etc.

****************************************************

4) Some tips

The default plugin settings are optimal and give a picture as close as possible 
to a real PSX. If you don't understand what the setting does, better not 
touch/change it.

16-bit modes are much faster and require less resources than 32-bit ones. If 
you experience low framerate, try to switch your desktop into the 16-bit mode.

You can activate FPS limitation if your game is running too fast. You can use 
"Auto-detection FPS limit", if you are not sure, what limit would be best to 
use. Or you just type in a FPS rate that suits you. 50 and 59.95 frames per 
second for PAL and NTSC games, respectively.

If you don't have enough money to buy a modern PC - buy a used PlayStation, 
those things are cheap. :P

****************************************************

5) Known problems

When set to "Power saver" profile some systems experience a noticeable drop in 
fps due to CPU frequency restricted to low values even under heavy load. It 
makes sense to try to switch to "Balanced" or even "High Performance" modes, or 
to turn the power saving off at all.

The GPU plugin needs a closer interaction with the emulator core than this. The 
current API is insufficient for a full-fledged emulation.

****************************************************

6) License

This program is freeware and cannot be sold. Also this program cannot be 
distributed without written permission. This program cannot be used for any 
commercial purposes. You may not reverse engineer, decompile, or disassemble 
the enclosed software. Authors are not responsible for any damages that this 
program may cause, and are also not responsible for anything this plugin will 
be used for.

****************************************************

7) Contacts

http://forum.emu-russia.net
irc://irc.newnet.net:6667/emu-russia
mailto:edgbla@yandex.ru

****************************************************
