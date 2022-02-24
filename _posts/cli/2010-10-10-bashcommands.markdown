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

rsync (simulation mode -n and verbose -v)
: ~~~sh
    $ rsync -rtazhn -v --delete \
    --exclude="dir1" \
    --exclude="dir2/file" \
    $ORIGIN_DIR/ root@192.168.0.100:/$DEST_DIR
~~~

> see rsync examples [here](https://www.tecmint.com/rsync-local-remote-file-synchronization-commands)

ssh
: ~~~sh
    $ ssh usuario@10.0.16.29 -p 222
~~~

scp
: ~~~sh
    $ scp -P 222 myfile.sql user@10.0.16.29:/home/user
~~~

Copy directory remotely
: ~~~sh
    $ scp -r mylocaldir user@10.0.16.29:/home/user
~~~

ssh login without password and scp autocompletion (with zsh)
: ~~~sh
    # do not enter a passphrase when prompted
    $ ssh-keygen
    # append the public key generated to remote server
    $ cat .ssh/id_rsa.pub | ssh <remote_user>@<remote_IP> 'cat >> .ssh/authorized_keys'
~~~

Uncompress tar.gz/tar.bz2
: ~~~sh
    $ tar -xz[v]f file.tar.gz / tar -xjf[v] file.tar.bz2
~~~

Compress and tar
: ~~~sh
    $ tar -[z|j]cvf archive_name.tar.[gz|bz2] directory_to_compress
~~~

Assign default directories permissions
: ~~~sh
    $ find . -type d -print0 | xargs -0 chmod 0755 # for directories
~~~

Assign default files permissions
: ~~~sh
    $ find . -type f -print0 | xargs -0 chmod 0644 # for files
~~~

2 ways of deleting matching files
: ~~~sh
    $ find . -name *flac  -print -exec rm {} \;
    $ find . -newermt '2014-12-31' -print0 | xargs -0 rm -rf
~~~

Translate \n to null character
: ~~~sh
    $ find . -iname "*blabla*" | sort -r | tr '\n' '\0' | xargs -0 mplayer
~~~

Using % with xargs
: ~~~sh
    $ ls | xargs -I % echo %
~~~

Checking partitions disk space
: ~~~sh
    $ df -h
~~~

Checking physical directories size
: ~~~sh
    $ du -sh
    # ncurses du version (must install first)
    $ ncdu
~~~

Checking deleted files holding disk space (so we can kill the responsible app)
: ~~~sh
    $ lsof -nP | grep '(deleted)'
~~~

Massive renaming of files
: ~~~sh
    # test rename with -n
    $ rename -n 's/<search_pattern>/<replace_pattern>/g' *.txt
    # rename and print name of files renamed (only *.txt files)
    $ rename -v 's/<search_pattern>/<replace_pattern>/g' *.txt
    # rename files read via standard input
    $ find <search_directory> -iname '*.txt' | rename -v 's/<search_pattern>/<replace_pattern>/g'
~~~

> Patterns expect [Perl Compatible Regular Expressions](https://regex101.com/#pcre) (PCRE).

Burn image to usb drive
: ~~~sh
    # first find drive letter with blkid
    sudo blkid
    # write image to device
    sudo dd bs=4M if=/path/to/file.iso of=/dev/sd[drive letter] status=progress
~~~

# Shell config and reloading

Set shell
: ~~~sh
    $ chsh -s $(which zsh)
~~~

Configure terminal proxy (put on .bashrc/.zshrc for permanent use)
: ~~~sh
    $ export http_proxy="http://user:password@proxy-server:port"
    $ export https_proxy="https://user:password@proxy-server:port"
    $ export ftp_proxy="http://user:password@proxy-server:port"
    
    # without authentication one-liner
    $ export {http,https,ftp}_proxy="http://proxy-server:port"
~~~

Reload .bashrc/.zshrc
: ~~~sh
    $ source [.bashrc|.zshrc]
~~~

# Working with partitions

Mount device as user (without sudo)
: ~~~sh
    $ mount /mnt/my_device
~~~

> for the command above to work you need to create ```/mnt/my_device``` directory and put on /etc/fstab a line like:
>
> UUID="8574-1C11" /mnt/my_device vfat rw,noauto,user,noexec 0 0
>
> * UUID can be found with ```blkid``` command
> * to automount at startup do not specify ```noauto``` option parameter (then you can umount manually with ```umount /mnt/my_device```)

Remount partition with write permissions
: ~~~sh
    # mount root partition with write permissions
    $ sudo mount -o remount,rw /
~~~

RAID1
: ~~~sh
    # create RAID1 device with 3 disks
    $ sudo mdadm -C /dev/md0 --level=raid0 --raid-devices=3 /dev/sdc1 /dev/sdd1 /dev/sde1
    # copy output from command and put in conf file /etc/mdadm/mdadm.conf
    $ sudo mdadm -Db /dev/md0
    # start all arrays from conf file
    $ sudo mdadm --assemble --scan
    # final step: create partition from device /dev/md0 and mount it
~~~

> More info on how to start array and RAID in general [here](https://www.digitalocean.com/community/tutorials/how-to-manage-raid-arrays-with-mdadm-on-ubuntu-16-04#starting-an-array)

Add disks to RAID1
: ~~~sh
    $ sudo mdadm -A -R /dev/md0 /dev/sdX1 /dev/sdY1
~~~

<br />

---

# Package management (apt systems)

Shows package status, autocomplete only installed packages
: ~~~sh
    $ dpkg -s
~~~

Autocompletes with repos packages, formatted output, accepts wildcards '*php*'
: ~~~sh
    $ dpkg-query -l
~~~

Displays command name package
: ~~~sh
    $ dpkg-query -S `which mkvmerge`
~~~

Shows location of installed package files
: ~~~sh
    $ dpkg -L
~~~

Searches for a file in repos packages
: ~~~sh
    $ apt-file search
~~~

Searches on repos (installed packages or not)
: ~~~sh
    $ apt-file show
~~~

Resync with repos
: ~~~sh
    $ apt-file update
~~~

Show last installed packages
: ~~~sh
    sudo gunzip -d /var/log/dpkg.log.*gz
    cat /var/log/dpkg.log* | grep "\ install\ " | sort | ccze
~~~


