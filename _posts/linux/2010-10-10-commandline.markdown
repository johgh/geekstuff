---
layout: post
title:  "Desktop/general commands"
permalink:  "linuxcommands"
date:   2015-07-25 16:30:15
category: GNU/Linux
tags: Sysadmin
---
Create .desktop (gnome app launcher)
: {% highlight sh %}
    $ gnome-desktop-item-edit ~/.local/share/applications --create-new
{% endhighlight %}

Associate vlc app to some extensions
: {% highlight sh %}
    $ xdg-mime default vlc.desktop video/x-ogg video/x-ogm video/x-ogm+ogg video/x-real-video video/x-sgi-movie video/x-theora video/x-theora+ogg
{% endhighlight %}

Create mkv file (without changing codec)
: {% highlight sh %}
    $ mkvmerge -o "/media/bla/output.mkv" --title "videotitle" "input.mp4" --default-track 0  --sub-charset 0:ISO-8859-1 --language 0:spa "./subtitles.spa.srt" --language 1:en "./subtitles.eng.srt"
{% endhighlight %}

Change default app
: {% highlight sh %}
    $ mimeopen -d file.txt
{% endhighlight %}

Disable disk automount (don't ask to mount)
: {% highlight sh %}
    $ gsettings set org.gnome.desktop.media-handling automount false
    $ gsettings set org.gnome.desktop.media-handling automount-open false
{% endhighlight %}

Tilix shortcut (full-screen quake mode with session)
: {% highlight sh %}
    # this should be assigned to an accessible key like F1
    tilix --quake --full-screen --session="~/dotfiles/tilix.json"
{% endhighlight %}

Deluge daemon configuration
: {% highlight sh %}
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
{% endhighlight %}

Swap Caps_Lock and Control_L
: {% highlight sh %}
    # put these lines on .Xmodmap file (tested on xfce)
    remove Lock = Caps_Lock
    keycode 0x42 = Control_L
    add Control = Control_L 
{% endhighlight %}

Notify opening guake when phplog changes (showing "tailed" log on guake)
: {% highlight sh %}
    $ while inotifywait -e close_write /var/log/phplog; do guake -s 0; guake -t; done > /dev/null 2>&1 &
{% endhighlight %}

Ask password for decrypt drive in gui popup
: {% highlight sh %}
    $ encfs --extpass=/usr/bin/ssh-askpass /src/.cryptk_encfs/ ~/dest > /dev/null 2>&1
{% endhighlight %}

Graphical rotation
: {% highlight sh %}
    $ xrandr -x / xrandr -y / xrandr -x -y / xrandr -o normal / xrandr -o inverted
{% endhighlight %}

Add app to startup
: {% highlight sh %}
    $ cp /usr/share/applications/guake.desktop ~/.config/autostart/
{% endhighlight %}

Move app to workspace at startup
: {% highlight sh %}
    $ gsettings set org.gnome.shell.extensions.auto-move-windows application-list "['banshee-media-player.desktop:2', 'deluge.desktop:2', 'rhythmbox.desktop:2', 'google-chrome.desktop:1', 'firefox.desktop:1']"
{% endhighlight %}

Configure default java version
: {% highlight sh %}
    $ update-alternatives --config java
{% endhighlight %}

