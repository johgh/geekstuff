---
layout: post
title:  "Bash commands"
permalink:  "bash commands"
date:   2011-07-15 16:30:15
category: CLI
tags: Sysadmin
---
# Commands

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

Set shell
: {% highlight sh %}
    $ chsh -s $(which zsh)
{% endhighlight %}

<br />

---

# Aliases

> Tested in bash and zsh.

> Save this file in your HOME directory and put the following line in your .bashrc or .zshrc file:
    ```. $HOME/<alias_file_name>```


{% github_sample_ref johgh/dotfiles/blob/master/.alias_functions  %}
<div> <button class="selectButton" data-id="#selectText1" type="button">Select text </button> </div>
<div id="selectText1">
{% highlight bash %}
{% github_sample johgh/dotfiles/blob/master/.alias_functions %}
{% endhighlight %}
</div>


<script src="{{ "/scripts/selecttext.js" | prepend: site.baseurl }}"></script>

