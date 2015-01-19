3dfsb
=====

3D File System Browser - cleaned up and improved fork of the old tdfsb which runs on GNU/Linux and should also run on BeOS/Haiku and FreeBSD.

E-mail: tomvanbraeckel+3dfsb@gmail.com

Homepage: https://github.com/tomvanbraeckel/3dfsb

Forked, cleaned up and improved by Tom Van Braeckel, originally written by Leander Seige.

Improvements made so far
************************

Major changes
-------------
- Extended audio and video support: more than 100 additional container formats and decoders are now supported through the latest GStreamer 1.4.3
- Better file identification: filetype is now determined by the contents of the file (with libmagic) with the extension of the file as a fallback
- High-resolution video previews: cranked up from the old 256x256 pixels to however high your graphics card supports (eg: 8192x8192)
- More fun: you can now zap away at your files with the lasergun tool! For your own protection, nothing is physically deleted from disk, unless y
ou explicitly configure the program to do so.
- Video input device (eg: webcam) file previews: Video4Linux (V4L2) capture devices are now visible in the 3D world and can be viewed just like your movies!
- No more waiting: fly into your directories instantly, with file previews being loaded asynchronously in the background

Minor changes
-------------
- Faster navigation by default
- Visible on-screen info by default
- Uncapped framerate by default
- Uncapped texture size by default
- Higher rendering resolution by default
- Lots and lots of code cleanups, bugfixes and comments added
- No more dependency on libsmpeg

Performance
-----------
This version runs at 1920x1080 resolution while playing 720p H264 video (2048x2048 texture) on a single-core of the Intel Core i7 at 2.90Ghz.

Screenshots
===========
![Screenshot: all major audio and video formats are supported through GStreamer. Video texture size went up from 256x256 to however high your GPU can go. Think 8192x8192.](/screenshots/01_videos.png?raw=true "High-resolution video previews")
*Above: all major audio and video formats are supported through GStreamer. Video texture size went up from 256x256 to however high your GPU can go. Think 8192x8192.*

![Screenshot: hardware device files (such as webcams) are visible in the 3D world and can be accessed from it.](/screenshots/02_webcam.png?raw=true "Hardware device file video capture")
*Above: hardware device files (such as webcams) are visible in the 3D world and can be accessed from it.*

![Screenshot: filetype detection is much more robust and versatile, relying on libmagic to identify a filetype by its contents. The old method, which is based on filename extensions, is used as a fallback.](/screenshots/03_image.png?raw=true "Improved filetype detection")
*Above: filetype detection is much more robust and versatile, relying on libmagic to identify a filetype by its contents. The old method, which is based on filename extensions, is used as a fallback.*

![Screenshot: you can use different tools to operate on your files, for example: blast them with the laser to delete them! And don't worry: for safety reasons, the program doesn't actually delete them from your disk unless you explicitly configure it to do so.](/screenshots/04_laser_weapon_tool.png?raw=true "Laserweapon tool to delete your files")
*Above: you can use different tools to operate on your files, for example: blast them with the laser to delete them! And don't worry: for safety reasons, the program doesn't actually delete them from your disk unless you explicitly configure it to do so.*

USAGE
=====

3dfsb

  or
  
3dfsb --version

  or
  
3dfsb -D /path/to/dir

  or
  
3dfsb --dir /path/to/dir

- the config file is $HOME/.3dfsb (e.g. /home/user/.3dfsb). if it does not
  exist tdsfb will generate one with all available options. this is strongly
  recommended.

- if you start the 3dfsb the first time, press 'h' for the help menu
  (will also be printed to the terminal)

- simply walk into the spheres for cd'ing into another directory

- select an object by pointing at it with the crosshair and press the left
  mouse button. or hold the left mouse button and press any key to select
  the first object that begins with that character (case sensitive).
    -   while an object is selected press the right mouse button simultaneously to
        automatic approach the object
        [unfortunately doesn't work on BeOS/Haiku as well as resizing the window, afaik
        these are issues of the SDL implementation, use the right CTRL for now].
    -   if an mp3 or mpeg1 video file is selected press the RETURN key to start
        the playback

- some of the displays are not visible while the help display is active

- it is possible to execute a custom command from within 3dfsb. configure
  your command in the config file! the command can be called by pressing
  the tabulator key. put a "%s" in the command line, this will be replaced
  by the current directory or selected file.
  for instance if you set the command to
    xmms "%s" &
  and press tab from a directory, xmms will be started with the directory
  given as argument. 
  if you select an audio file and press the tab key xmms will play the file.
  the default command is
    cd "%s"; xterm&
  it will open a xterm in the current directory.
  this command is always present by pressing shift+tab!
  so you have two commands: 
  - one by configuring your custom command for the tab key
  - one by pressing shift+tab, it will execute the built in xterm call  
  but dont forget the quotation marks!
  you are free to not add "%s" to your custom command if you just
  want to launch any program. but if you do so, you can customize
  3dfsb for your needs, choose a certain kind of files and than launch
  emacs for editing text files, mplayer for playing avis or whatever...

You may change the default settings (including keyboard configuration) by editing ~/.3dfsb

Dependencies
============

Compilation libraries:
----------------------
You need imagemagick's "mogrify" tool to convert the built-in image files to pnm files.

Hint: sudo apt-get install imagemagick

Development libraries:
----------------------
You may need to install 'devel' packages of these
libraries in order to get the necessary .h files
and the sdl-config script.

- SDL: http://www.libsdl.org
- SDL_image: http://www.libsdl.org/projects/SDL_image/index.html
- OpenGL/GLU/glut: Linux/FreeBSB users can use their package manager, BeOS/Haiku users should have OpenGL (including GLU) included. For glut look at http://www.bebits.com/
- GSteamer 1.xx Core, Gstreamer 1.xx plugins: http://www.gstreamer.com/
- libmagic-dev: for mimetype identification

On Ubuntu, you can install all build-time dependencies with:

sudo apt-get install build-essential freeglut3-dev libsdl-image1.2-dev libsdl1.2-dev libxi-dev libxmu-dev libmagic-dev imagemagick

For GStreamer, you need:
sudo apt-get install libgstreamer1.0-dev libgstreamer-plugins-base1.0-dev libgstreamer-plugins-bad1.0-dev

And if you want all GStreamer codecs and plugins, use:

sudo apt-get install gstreamer1.0-plugins-* gstreamer1.0-libav

(And for pulseaudio, but this is not being used currently but might be someday: sudo apt-get install gstreamer1.0-pulseaudio)

Compilation
===========

There is a small shell script which contains a standard compile string for every OS (Linux, BeOS and BSD).
So please try:

./compile.sh

Alternatively, CMake can be used to compile.
For this, try:

cmake .
make

If the compilation was successful you can call the 3dfsb:

./3dfsb


ADDITIONAL NOTES
================

FreeBSD:

If you have problems with SDL_image try:
cd /usr/ports/graphics/sdl_image/
make install


BeOS/Haiku:

This package does not contain a BeOS binary, because I don't 
have BeOS/Haiku installed on my computer anymore.

The source should compile anyway.

NVidia Cards under Linux (+FreeBSD?)
------------------------------------

NVidia users who have problems compiling the 3dfsb are often linking
against the wrong libraries, especially the libGLU.so.
In this case please read the instructions that came
with your drivers.
The following often helped but of course i can give no
guarantee, try it on your own risk!
    There are two libGLU.so's. Move the original libGLU.so
    to a safe place (libGLU.so.my.original or something).
    Make a link libGLU.so->libGLU.so.the.right.one.
    libGLU.so.the.right.one is often >500kByte while
    the wrong libGLU.so is much smaller.




CREDITS
=======
Maintained, improved and cleaned up by Tom Van Braeckel.

Thanks go out to:
- Leander Seige for building the original tdfsb program
- Marc Berhault for some additional code (see ChangeLog)
- Nico 'aMadMan' Toerl for extensive beta testing
- Kyle 'greenfly' Rankin for some additional code (see ChangeLog)
- Benjamin Burke for help and testing of the compile.sh
- Rafal Zawadzki for creating man pages and debian packages

History
=======
25/12/2014:
Tom Van Braeckel here; I've picked up where Leander left off.
I'm cleaning up the code and adding features, see CHANGELOG!

22/06/2007:
Leander Seige: "TDFSB is 6 years old now and I havent done anything on it for a long time.
Today I would code a lot of things very different - better i hope - than years
ago. But, so what, it still works and I got very less bug reports on 3dfsb.
Some days ago I installed Gentoo for the first time and I heared that someone
(thank you!) build a package for Gentoo so I tried emerge 3dfsb and it worked :)
Besides that it has problems with freeglut which I quickly fixed now.
So I hope some people, YOU, still like it. Have fun!"

