---
layout: post
title:  "Desktop/general commands"
permalink:  "linuxcommands"
date:   2015-07-25 16:30:15
category: GNU/Linux
tags: Sysadmin
---
Create .desktop (gnome app launcher)
: ~~~sh
    $ gnome-desktop-item-edit ~/.local/share/applications --create-new
~~~

Associate vlc app to some extensions
: ~~~sh
    $ xdg-mime default vlc.desktop video/x-ogg video/x-ogm video/x-ogm+ogg video/x-real-video video/x-sgi-movie video/x-theora video/x-theora+ogg
~~~

Create mkv file (without changing codec)
: ~~~sh
    $ mkvmerge -o "/media/bla/output.mkv" --title "videotitle" "input.mp4" --default-track 0  --sub-charset 0:ISO-8859-1 --language 0:spa "./subtitles.spa.srt" --language 1:en "./subtitles.eng.srt"
~~~

Change default app
: ~~~sh
    $ mimeopen -d file.txt
~~~

Disable disk automount (don't ask to mount)
: ~~~sh
    $ gsettings set org.gnome.desktop.media-handling automount false
    $ gsettings set org.gnome.desktop.media-handling automount-open false
~~~

Tilix shortcut (full-screen quake mode with session)
: ~~~sh
    # this should be assigned to an accessible key like F1
    tilix --quake --full-screen --session="~/dotfiles/tilix.json"
~~~

Deluge daemon configuration
: ~~~sh
    # FROM SERVER:
    $ sudo apt-get install deluged
    # add to startup /usr/bin/deluged (with gnome-session-properties for example)
    # edit ~/.config/deluge/auth and add extra line:
    <user>:<pass>:10
    # Disable classic mode from GTK client and test 127.0.0.1:58846 from 'Connection Manager' 
    # FROM CLIENT:
    $ sudo apt-get install deluge
    # configure from 'Connection manager':
    <user>@<server_ip>:58846 # with user/pass specified on ~/.config/deluge/auth from server
~~~

Swap Caps_Lock and Control_L
: ~~~sh
    # put these lines on .Xmodmap file (tested on xfce)
    remove Lock = Caps_Lock
    keycode 0x42 = Control_L
    add Control = Control_L 
~~~

Notify opening guake when phplog changes (showing "tailed" log on guake)
: ~~~sh
    $ while inotifywait -e close_write /var/log/phplog; do guake -s 0; guake -t; done > /dev/null 2>&1 &
~~~

Ask password for decrypt drive in gui popup
: ~~~sh
    $ encfs --extpass=/usr/bin/ssh-askpass /src/.cryptk_encfs/ ~/dest > /dev/null 2>&1
~~~

Graphical rotation
: ~~~sh
    $ xrandr -x / xrandr -y / xrandr -x -y / xrandr -o normal / xrandr -o inverted
~~~

Add app to startup
: ~~~sh
    $ cp /usr/share/applications/guake.desktop ~/.config/autostart/
~~~

Move app to workspace at startup
: ~~~sh
    $ gsettings set org.gnome.shell.extensions.auto-move-windows application-list "['banshee-media-player.desktop:2', 'deluge.desktop:2', 'rhythmbox.desktop:2', 'google-chrome.desktop:1', 'firefox.desktop:1']"
~~~

Configure default java version
: ~~~sh
    $ update-alternatives --config java
~~~

