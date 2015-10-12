---
layout: post
title:  "Commands"
permalink:  "commands"
date:   2015-07-25 16:30:15
category: Linux
tags: Sysadmin
---
# General commands

> For a complete generic command reference go [here](http://cb.vu/unixtoolbox.xhtml)

ssh
: {% highlight sh %}
    $ ssh usuario@10.0.16.29 -p 222
{% endhighlight %}

scp
: {% highlight sh %}
    $ scp -P 222 D2System_venus.sql usuario@10.0.16.29:/home/usuario
{% endhighlight %}

Uncompress tar.gz/tar.bz2
: {% highlight sh %}
    $ tar -xz[v]f file.tar.gz / tar -xjf[v] file.tar.bz2
{% endhighlight %}

Compress and tar
: {% highlight sh %}
    $ tar -[z|j]cvf archive_name.tar.[gz|bz2] directory_to_compress
{% endhighlight %}

Assign default directories permissions
: {% highlight sh %}
    $ find . -type d -print0 | xargs -0 chmod 0755 # for directories
{% endhighlight %}

Assign default files permissions
: {% highlight sh %}
    $ find . -type f -print0 | xargs -0 chmod 0644 # for files
{% endhighlight %}

2 ways of deleting matching files
: {% highlight sh %}
    $ find . -name *flac  -print -exec rm {} \;
    $ find . -newermt '2014-12-31' -print0 | xargs -0 rm -rf
{% endhighlight %}

Translate \n to null character
: {% highlight sh %}
    $ find . -iname "*blabla*" | sort -r | tr '\n' '\0' | xargs -0 mplayer
{% endhighlight %}

Using % with xargs
: {% highlight sh %}
    $ ls | xargs -I % echo %
{% endhighlight %}

Reload .bashrc/.zshrc
: {% highlight sh %}
    $ source [.bashrc|.zshrc]
{% endhighlight %}

Mount device as user (without sudo)
: {% highlight sh %}
    $ mount /mnt/my_device
{% endhighlight %}

> for the command above to work you need to create ```/mnt/my_device``` directory and put on /etc/fstab a line like:
>
> UUID="8574-1C11" /mnt/my_device vfat rw,noauto,user,noexec 0 0
>
> * UUID can be found with ```blkid``` command
> * to automount at startup do not specify ```noauto``` option parameter (then you can umount manually with ```umount /mnt/my_device```)

Public IP
: {% highlight sh %}
    $ curl ifconfig.me
{% endhighlight %}

Set shell
: {% highlight sh %}
    $ chsh -s $(which zsh)
{% endhighlight %}

Configure java
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

<br />

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

<br />

---


# Alias

Open file with associated gui app
: {% highlight sh %}
    openapp(){ nohup xdg-open $1 > /dev/null 2> /dev/null }; alias o=openapp
{% endhighlight %}

Force pull
: {% highlight sh %}
    alias gpull='git commit -a; git pull'
{% endhighlight %}

Force push
: {% highlight sh %}
    alias gpush='git commit -a; git push'
{% endhighlight %}

Difftool with origin/master
: {% highlight sh %}
    alias gdiff='git difftool origin/master'
{% endhighlight %}

Mergetool
: {% highlight sh %}
    alias gmerge='git mergetool'
{% endhighlight %}

LS alias
: {% highlight sh %}
    alias ll='ls -alF'
    alias la='ls -A'
    alias l='ls -CF'
    alias lt='ls -lrt'
{% endhighlight %}

Short sudo
: {% highlight sh %}
    alias s='sudo'
{% endhighlight %}

Repeat last command with sudo
: {% highlight sh %}
    alias fuck='sudo !!'
{% endhighlight %}

Shutdown, reboot, suspend
: {% highlight sh %}
    alias shutdown='sudo shutdown –h now'
    alias restart='sudo shutdown –r now'
    alias suspend='sudo pm-suspend'
{% endhighlight %}

> on /etc/sudoers:
> user ALL=(ALL) NOPASSWD: /usr/sbin/pm-suspend
> user ALL=(ALL) NOPASSWD: /sbin/shutdown

Mount formatted
: {% highlight sh %}
    alias mountt = 'mount |column -t'
{% endhighlight %}

Apt alias
: {% highlight sh %}
    alias inst='sudo apt-get install'
    alias search='apt-cache search'
    alias purge='sudo apt-get purge'
    alias remove='sudo apt-get remove'
    alias update='sudo apt-get update'
    alias upgrade='sudo apt-get dist-upgrade'
    alias show='sudo apt-cache show'
{% endhighlight %}

