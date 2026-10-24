Update 24Oct2026: For these instructions to work, download and install the 2021-10-30 Raspios Bullseye found here: 
https://ftp.jaist.ac.jp/pub/raspberrypi/raspios_full_armhf/images/raspios_full_armhf-2021-11-08/

You can follow along with my video found here:   
https://youtu.be/f05ztYR7nSI    

I use a monitor with a Raspberry Pi to make a digital frame using Dynaframe. I show the steps to install the Raspberry Pi OS, share a USB drive on the pi with the network, and install Dynaframe. Now all my cool QSL cards are displayed.

Steps in Order: (You may want to copy/paste items after Type This:) 
01. Assemble the Raspberry Pi including heat sinks and added shims
02. Download Belena Etcher to format  https://www.balena.io/etcher/
03. Download the current Raspberry Pi OS. I got the "Raspberry Pi OS with desktop and 
      recommended software" found at 
 https://www.raspberrypi.com/software/operating-systems/
04. Use Belena Etcher to format the sd card.
05. Next, Country, language, timezone, change password, setup wifi, and update the pi, wait and 
      reboot
06. Navigate the menu to Preferences then Raspberry Pi Configuration
 Change the hostname here to something cool like ShackFrame (I used QslShow)
 In the Display tab, disable Screen Blanking
 click ok and reboot
07. First program: "gnome-disk-utility" Go to menu, Preferences, Add/Remove Software
 Search for this file and install
08. Plug in the USB Drive you want to erase. Find the "Disks" program in the menu and run it.
09. Make sure you select the USB drive on the left!! Delete any partitions on the USB
 Create a partition on the unallocated space name it USBDrive (anything)
 Be sure to select "For use with all...(FAT)" [create]
 Note the dev thingy here. If it's the only partition on the drive it will be /dev/sda
10. Open a terminal window found at the top Type this: 
       sudo nano /etc/fstab
 Arrow down to the bottom line without deleting anything (use your dev/sda name)
 Type this: /dev/sda /mnt/MyPictures vfat defaults,umask=0000,nofail 0 0
 (these are all zeros with spaces before each at the end. I added an extra zero to the umask, it 
       may have no affect but what the hay.)
 To exit and save in nano we hold control to type x, then type y for yes, then hit enter to keep
 the same file name. 
11. When at the prompt again, Type This: sudo reboot
12. After the reboot we want to check our folder. Open the File Manager at the top. Navigate and 
      click on mnt. Right click on the MyPictures folder. Select Properties. Select the permisions 
      tab. All these should read "Anyone" If they don't repeat step 10 and correct your error.
13. Open a terminal window Type this: sudo apt-get install samba
 Hit enter and type y for yes when prompted. When finished
 Type This: sudo nano /etc/samba/smb.conf
 Arrow down to the bottom of this file without deleting anything.
 At the bottom left we will add the name of the share then tab the rest so it looks like this:
 [FramePics]
  Path = /mnt/MyPictures
  read only = no
  public = yes
  writable = yes
  guest ok = yes
 To exit and save in nano we hold control to type x, then type y for yes, then hit enter to keep
 the same file name. 
14. When at the prompt again, Type This: sudo reboot
15. From another computer: In Windows open File Explorer and in the address bar at the top 
 Type This: \\QslShow 
  (Instead of Qslshow this would be the hostname you picked in step 6)
 You should be able to see the FramePics folder, open it, create a new file, and delete it. 
 If not, repeat step 13. Add a few pictures to this folder now.

16. Back at the Pi, open a terminal window. (Add "https:" in place of ~) 
sudo wget ~//github.com/Geektoolkit/Dynaframe3/releases/download/2.19/install.sh && bash install.sh; rm -f install.sh ; sudo reboot

17. After reboot and about 10 seconds you should see a black Dynaframe screen. 
 Without typing anything else: hit escape. Using the file Manager navigate to the Dynaframe 
      Folder. Scroll to run.sh and right click to copy it. Now right click on the desktop to paste it. 
 Mouse over your wifi at the top for your ip address if you want but we will use the hostname 
      like we did earlier. Double click the run.sh file and choose Execute. 
18. At another computer: In Windows open a browser Type This: Qslshow:8000
 (this is your hostname from step 6 so it could be Shackframe:8000)
 You should be directed to the Dynaframe page on the Raspberry Pi
19. Click the second tab called "playlists" in the "Add Directory" box 
 Type This: /mnt/MyPictures
 Click Save. You should see this folder added above.
20. Click on Controls
 Click on "Update file list" and then click next. You should see a picture from the usb drive. 
 I changed my transition duration during fades in settings to 3000. 
 Double sticky tape this up to the back of the monitor to look nice and ENJOY! 

The Dynaframe video about the new features is here:  https://youtu.be/XEaUsaNEzjY

The Dynaframe github can be found at https://github.com/Geektoolkit/Dynaframe3

The Canakit Raspberry Pi 3B+ for $120 is here: https://www.canakit.com/raspberry-pi-3-ultimate-kit.html

73, Scott KD4SIR










# Dynaframe 2

--------------------------NOTE--------------
--------------------------NOTE----------------

This project is deprecated. I leave it here so that it's available as source for anyone that wants to learn from it, but it no longer works. The software was tightly integrated with VLC, and VLC changed drastically after this, so it requires a 5 year old OS (Buster) to try to work.

There are 2 roads to get something to work:
1) If you're linux saavy, you can try the [pi3D project by paddy](https://pypi.org/project/picframe/) picframe project.

2) If you're looking for a simple 'image it and make it an awesome picture frame with sync abilities, plugins and more' then Dynaframe still exists as a paid project ($60 if you catch it during alpha, $99 afterwards)
It's available at http://dynaframe.pro

It has video transitions, plugtins, a store, a simple updater, NFC, MQTT and automatio support, scheduled playlists and shutdowns, shader transitions and more.

Thankyou for all of those taht supported me for years and allowed this to build where I could leave my job and make this my full time job to do what I truly love...make crazy cool digital media frames!

--------------------------NOTE----------------
--------------------------NOTE----------------

Dynamic Photo and Video Slideshow system for SBC (such as Raspberry pi)

Note: There is now a Dynaframe Pro, which is a patreon supported successor to this. This project will continue to live on as the open source/free DIY version, but if you're looking for a simpler supported product, then Dynaframe Pro is where I've put that work. It includes skinning, image based installs, and more!  Find out more and how to get it here: https://www.youtube.com/watch?v=CIwkHq_v-ZE

Video Demo, how to install, and intro here: https://youtu.be/XEaUsaNEzjY
There are other related videos on the same channel.
There are user written tutorials in Show and Tell under Discussions

Note: Please see the releases section for the latest release. The below command will install 2.13 which I consider stable, but there are more features in later releases if you'd like to try them. To remove a release just delete the folder using "sudo rm -rf Dynaframe" and rerun the install script.

Quickstart: On a raspberry pi based system you'll want to connect to a network, put a few images in the Pictures folder to get started, and then run:

    sudo wget https://github.com/Geektoolkit/Dynaframe3/releases/download/2.19/install.sh && bash install.sh; rm -f install.sh ; sudo reboot
    
On reboot it should startup, and it'll show you the URL of the configuration page.

To exit, please hit the 'esc' button.  

To restart on a raspberry pi, you can launch it again using ./Dynaframe 

Hardware Requirements:
I recommend a Raspberry pi 3B+ or better. It really shines on a Pi4 2gig or better.
A heatsink is required...this gets VERY CPU intensive when transitioning, and fast transitions will thermal the pi and bring up the temp gauge.
OpenGL acceleration needs to be OFF! You can find this using sudo raspi-config and ensuring it's set to 'legacy' under opengl settigs.
I recommend either a FLIRC style case, a good heatsink solution, or a small fan for active cooling.  
Adding memory to the GPU and slowing down the time between transitions (as well as speeding up the transition time) can help with cooling if needed.

Additional steps to clean up some things:
1) To get rid of the mouse cursor, you'll want to install unclutter.  sudo apt-get install unclutter, and then run: unclutter -idle 0
2) To prevent screen blanking, please run: sudo raspi-config, and then turn off screen blanking in the menus there under Display Options I'm working on getting these into the setup scripts.




Welcome to Dynaframe!  Dynaframe was designed to be a simple photo and video slideshow viewer.  I wanted to have something that could do slideshows but also show 'plotagraphs', which are essentially animated images.  I use an app on iOS called 'Werble' which made some really cool ones, but there wasn't a good way to show them off.

The first version of Dynaframe was simply a python script that went through a folder list and then executed feh or omxplayer base don the file extension.  This was buggy, unstable, ugly, and in the end I abandoned it, however I had a ton of requests for updates and features. I decided to rewrite it in Avalonia, and that has proven to make things MUCH better.  The feature set increased dramatically, and every time I get a few hours to work on it I add a few more.  currently there are:
Features:
1) crossfades - Image to image will now crossfade (vs. v1 where they simply appeared)
2) Fullscreen - You no longer have to hide the task bar and black out the background...this will automaticlaly take up the full screen
3) persistent settings - Changes made via the web UI will now be saved
4) Rotation! - You no longer have to rotate the OS, you can rotate on the fly and save the setting for the slideshow (per image rotation is not supported)
5) All photos - instead of being limited to photos in a single folder, all photos in your 'my pictures' folder or equivalent will now be able to be selected
6) Scaling - If your image doens't take up the full screen, it'll now automatically be zoomed to fill the frame
7) Smaller Download size - V1 was a 16 gig Raspbian image, this is under 60 megs!
8) No need to hide the background - This was something that had to be done in V1. No longer! The background is covered by the app
9) Easier 'autostart' setup - This now sets up the 'run on startup' for you as part of the installer
10) Uses pictures folder - This allows for more updates without having to worry about losing your slideshow/setups. It also is easier to get pictures into the pictures folder than a proprietary one
11) Shutdown from webui - You can now shut the frame off! Since the frame may not have a keyboard/mouse hooked up to it, being able to safely shut it off is handy
12) custom slide times - You can now, without editing code, select the time you want photos to be on the frame between transitions
13) custom transition times - If you want a quick cross fade, or a looong slow one, you can now do that.  I find that 30 second crossfades are VERY cool effects..try it!
14) Filetype support - It's very easy to now add image and video type supports. This already supports more files than V1, and I'll keep adding more! For videos MPEG, MP4, MOV, AVI are all supported
15) Filename fixes - V1 had a very buggy situation with filenames...underscores, dashes, and other characters would wreck it.  In this version this is all fixed!
16) Infobar - You can now choose to have a date, a time, both, or a file name displayed. The font size and type are configurable
17) Ease of use improvements - Besides all of the stuff above, it now shows the IP/port of the webserver when it's started, so that it's easy for users to load the settings page on thier phone
18) Web frontend for settings - A simple web frontend is supplied so that settings can be loaded easily. They persist.  And being a simple webpage means no app to install, and works on just about any device
19) Playlists - You can put pictures in folders and play them as 'playlists' which allows you to sort your pictures and show them in ways that usually aren't possible when using standard slideshow software (without restarting everything). You can also 
20) Raspberry pi only - You can now control most monitors via the webUI - This allows you to turn the monitor on/off from the pi.
21) Ability to add folders - This allows you to use any folder you want, including ones mounted from NAS, WebDav, or USB drives. 


Question: What happened to Dynaframe 2? 
  Dynaframe 2 was a WIP that I never shipped. I worked on it using the pi3D library, and just never got it off the ground. I call this Dynaframe2, but the repo is titled Dynaframe3 since 2 is now 'taken'.
  
  Q: What's next for this project?
    I have a few 'hot' features I want to get in.  These include:
    1) EXIF data - I think having the ability to mark up images with data such as where its taken, or the story behind it, would be handy, esp. if being used as a family photo frame.  I want to have a way to show that data
    2) DONE - font settings - I'd like to have the front for the clock, and future uses, have settings
    3) Weather/RSS feeds - There is the ability to easily turn on text...it'd be useful to have that get other data such as possibly a stock quote, weather, calendar info, or an RSS feed
    4) Gesture/keypad/ir remotes - I'd like to have support for methods to control the panel, for instance an IR Remote could let someone enter thier wifi account info possibly
    5) customizable keys - I'd like to enable keyboard shortcuts for those that do have keyboards connevcted, and to start then shimming in Gestures and other control methods built on top of that
 
 
 Compiling:
   This is built on Avalonia in VS 2019 (.10 Preview 6), and the dotnet core SDK.  The dependancies should come down via Nuget.
 
 Thankyou for taking a look at my project. To simply install it on a raspbery pi, you can launch one of the following (if you're not installing on a pi, you'll likely have to compile it for now. I'll make differnet releases based on demand.

(This one autoreboots at the end)
sudo wget https://github.com/Geektoolkit/Dynaframe3/releases/download/2.13/install.sh && bash install.sh; rm -f install.sh ; sudo reboot

If you want to keep the install.sh around to poke at it and not reboot, you can also try:
sudo wget https://github.com/Geektoolkit/Dynaframe3/releases/download/2.13/install.sh && bash install.sh

Thankyou. Please file issues as you find them and I'll do what I can. This is a side project for me.


