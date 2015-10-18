---
layout: post
title:  ".gitconfig"
permalink:  "gitconfig"
date:   2015-07-11 16:30:15
category: CLI
tags: Sysadmin
---

> This `.gitconfig` sample file is intended to be used as the global configuration for all git repositories cloned in a machine. So it should be place in `$HOME` directory.

> Coincidental configurations in a `.gitconfig` file of a particular repository will override these values. Execute `git config -l` to see the real configuration applied in a repository.

> To add additional configurations to this file use the `--global` parameter, like so: `git config --global user.name "John Doe"`. To delete configurations edit the raw file.

<script src="{{ "/scripts/selecttext.js" | prepend: site.baseurl }}"></script>

{% github_sample_ref johgh/dotfiles/blob/master/.gitconfig %}

<div> <button class="selectButton" data-id="#selectText1" type="button">Select text </button> </div>
<div id="selectText1">
{% highlight bash %}
{% github_sample johgh/dotfiles/blob/master/.gitconfig %}
{% endhighlight %}
</div>


