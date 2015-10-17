---
layout: post
title:  "Bootstrap"
permalink:  "bootstrap"
date:   2015-07-25 16:30:15
category: Web
tags: Web
---

## How to install Bootstrap-sass (compass)

Install ruby gems
: {% highlight bash %}
    $ sudo apt-get install ruby1.9.1-full nodejs
    $ sudo gem install bootstrap-sass
    $ sudo gem install sass
    $ sudo gem install compass
{% endhighlight %}

Install bootstrap in your project
: {% highlight bash %}
    # generate files
    compass create project-files -r bootstrap-sass --using bootstrap
    # install files
    cd ~/project-files/
    mv stylesheets css
    mv javascripts js
    mv * <your_public_dir>
{% endhighlight %}

Configure bootstrap sass compiler
: {% highlight bash %}
    css_dir = "css"
    javascripts_dir = "js"
    relative_assets = true
{% endhighlight %}


Add assets to your layout
: {% highlight jinja %}
{% raw %}
    <link href="{{ asset('css/styles.css') }}" rel="stylesheet" />
    <script src="{{ asset('js/bootstrap.min.js') }}"></script>
{% endraw %}
{% endhighlight %}


Compile on demmand
: {% highlight bash %}
    # change any .scss files like sass/_bootstrap-variables.scss
    $ cd <root_of_sass_project>
    $ compass compile
{% endhighlight %}

Autocompile
: {% highlight bash %}
    $ compass watch <root_of_sass_project>
{% endhighlight %}

> More info
: 
* [Bootstrap-sass documentation](https://github.com/twbs/bootstrap-sass)
* [Compass with assetic](http://alexandre-salome.fr/blog/Sass-Compass-Assetic-In-Ten-Minutes)
* [Sass reference](http://sass-lang.com/documentation/file.SASS_REFERENCE.html)
