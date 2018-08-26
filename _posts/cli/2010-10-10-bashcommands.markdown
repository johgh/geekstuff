---
layout: post
title:  "Bash/UNIX commands"
permalink:  "bash commands"
date:   2011-07-15 16:30:15
category: Terminal
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
    $ scp -P 222 myfile.sql user@10.0.16.29:/home/user
{% endhighlight %}

Copy directory remotely
: {% highlight sh %}
    $ scp -r mylocaldir user@10.0.16.29:/home/user
{% endhighlight %}

SSH login without password and scp autocompletion (with zsh)
: {% highlight sh %}
    # do not enter a passphrase when prompted
    $ ssh-keygen
    # append the public key generated to remote server
    $ cat .ssh/id_rsa.pub | ssh <remote_user>@<remote_IP> 'cat >> .ssh/authorized_keys'
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

Checking partitions disk space
: {% highlight sh %}
    $ df -h
{% endhighlight %}

Checking physical directories size
: {% highlight sh %}
    $ du -sh
    # ncurses du version (must install first)
    $ ncdu
{% endhighlight %}

Checking deleted files holding disk space (so we can kill the responsible app)
: {% highlight sh %}
    $ lsof -nP | grep '(deleted)'
{% endhighlight %}

Massive renaming of files
: {% highlight sh %}
    # test rename with -n
    $ rename -n 's/<search_pattern>/<replace_pattern>/g' *.txt
    # rename and print name of files renamed (only *.txt files)
    $ rename -v 's/<search_pattern>/<replace_pattern>/g' *.txt
    # rename files read via standard input
    $ find <search_directory> -iname '*.txt' | rename -v 's/<search_pattern>/<replace_pattern>/g'
{% endhighlight %}

> Patterns expect [Perl Compatible Regular Expressions](https://regex101.com/#pcre) (PCRE).

# Shell config and reloading

Set shell
: {% highlight sh %}
    $ chsh -s $(which zsh)
{% endhighlight %}

Configure terminal proxy (put on .bashrc/.zshrc for permanent use)
: {% highlight sh %}
    $ export http_proxy="http://user:password@proxy-server:port"
    $ export https_proxy="https://user:password@proxy-server:port"
    $ export ftp_proxy="http://user:password@proxy-server:port"
    
    # without authentication one-liner
    $ export {http,https,ftp}_proxy="http://proxy-server:port"
{% endhighlight %}

Reload .bashrc/.zshrc
: {% highlight sh %}
    $ source [.bashrc|.zshrc]
{% endhighlight %}

# Working with partitions

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

Remount partition with write permissions
: {% highlight sh %}
    # mount root partition with write permissions
    $ sudo mount -o remount,rw /
{% endhighlight %}

Add disks to RAID1
: {% highlight sh %}
    $ sudo mdadm -A -R /dev/md0 /dev/sdX1 /dev/sdY1
{% endhighlight %}

<br />

---

# Package management (apt systems)

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


