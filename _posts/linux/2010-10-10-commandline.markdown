---
layout: post
title:  "Linux commands"
permalink:  "linuxcommands"
date:   2015-07-25 16:30:15
category: Linux
tags: Sysadmin
---
# Apt commands

Shows package status, autocomplete only installed packages
: {% highlight sh %}
    $ dpkg -s
{% endhighlight %}

Autocompletes with repos packages, formatted output, accepts wildcards '*php*'
: {% highlight sh %}
    $ dpkg-query -l
{% endhighlight %}

Displays command name package
: {% highlight sh %}
    $ dpkg-query -S `which mkvmerge`
{% endhighlight %}

Shows location of installed package files
: {% highlight sh %}
    $ dpkg -L
{% endhighlight %}

Searches for a file in repos packages
: {% highlight sh %}
    $ apt-file search
{% endhighlight %}

Searches on repos (installed packages or not)
: {% highlight sh %}
    $ apt-file show
{% endhighlight %}

Resync with repos
: {% highlight sh %}
    $ apt-file update
{% endhighlight %}

Show last installed packages
: {% highlight sh %}
    sudo gunzip -d /var/log/dpkg.log.*gz
    cat /var/log/dpkg.log* | grep "\ install\ " | sort | ccze
{% endhighlight %}

<br />

---


# Desktop commands

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
    $ gsettings set org.gnome.shell.extensions.auto-move-windows application-list "['banshee.desktop:2','deluge.desktop:2','jdownloader.desktop:2']"
{% endhighlight %}

Configure default java version
: {% highlight sh %}
    $ update-alternatives --config java
{% endhighlight %}

Configure terminal proxy (put on .bashrc for permanent use)
: {% highlight sh %}
    $ export http_proxy="http://user:password@proxy-server:port"
    $ export https_proxy="https://user:password@proxy-server:port"
    $ export ftp_proxy="http://user:password@proxy-server:port"
    
    # without authentication one-liner
    $ export {http,https,ftp}_proxy="http://proxy-server:port"
{% endhighlight %}
