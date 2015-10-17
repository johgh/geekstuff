---
layout: post
title:  ".gitconfig"
permalink:  "gitconfig"
date:   2015-07-11 16:30:15
category: CLI
tags: Sysadmin Web
---

# Sample file


> This `.gitconfig` file is intended to be used as a global configuration for all git repositories on a machine.

<script src="{{ "/scripts/selecttext.js" | prepend: site.baseurl }}"></script>

{% github_sample_ref johgh/dotfiles/blob/master/.gitconfig %}

<div> <button class="selectButton" data-id="#selectText1" type="button">Select text </button> </div>
<div id="selectText1">
{% highlight bash %}
{% github_sample johgh/dotfiles/blob/master/.gitconfig %}
{% endhighlight %}
</div>


> Coincidental configurations in a `.gitconfig` file of a particular repository will override these values. To see the applied configuration to a certain repository execute: `git config -l`

> To add additional configurations to this file simply add the `--global` parameter to the git config command, like so: `git config --global user.name "John Doe"`. To delete configurations you can edit the raw file.

