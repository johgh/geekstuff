---
layout: post
title:  "Bootstrap"
permalink:  "bootstrap"
date:   2015-07-25 16:30:15
category: WebDev
tags: Web
---

## Bootstrap grid (3.3)

Bootrstrap media queries breakpoints
: {% highlight html %}
    /* Small devices (tablets, 768px and up) */
    @media (min-width: @screen-sm-min) { ... }
    /* Medium devices (desktops, 992px and up) */
    @media (min-width: @screen-md-min) { ... }
    /* Large devices (large desktops, 1200px and up) */
    @media (min-width: @screen-lg-min) { ... }
{% endhighlight %}

"row" class forces column breaks
: {% highlight html %}
<div class="row">
  <div class="col-md-8">.col-md-8</div>
  <div class="col-md-4">.col-md-4</div>
</div>
<div class="row">
  <div class="col-md-4">.col-md-4</div>
  <div class="col-md-4">.col-md-4</div>
  <div class="col-md-4">.col-md-4</div>
</div>
{% endhighlight %}

"container-fluid" provides total responsiveness
: {% highlight html %}
    <div class="container-fluid">
{% endhighlight %}

"container" provides 'step responsiveness'
: {% highlight html %}
    <div class="container">
{% endhighlight %}

Add extra clearfix for only the required viewport
: {% highlight html %}
<div class="row">
  <div class="col-xs-6 col-sm-3">.col-xs-6 .col-sm-3</div>
  <div class="col-xs-6 col-sm-3">.col-xs-6 .col-sm-3</div>
  <div class="clearfix visible-xs-block"></div>
  <div class="col-xs-6 col-sm-3">.col-xs-6 .col-sm-3</div>
  <div class="col-xs-6 col-sm-3">.col-xs-6 .col-sm-3</div>
</div>
{% endhighlight %}

Stack the columns on mobile by making one full-width and the other half-width
: {% highlight html %}
<div class="row">
  <div class="col-xs-12 col-md-8">.col-xs-12 .col-md-8</div>
  <div class="col-xs-6 col-md-4">.col-xs-6 .col-md-4</div>
</div>
{% endhighlight %}

You can also override offsets from lower grid tiers with .col-X-offset-0 classes.
: {% highlight html %}
<div class="row">
  <div class="col-xs-6 col-sm-4">
  </div>
  <div class="col-xs-6 col-sm-4">
  </div>
  <div class="col-xs-6 col-xs-offset-3 col-sm-4 col-sm-offset-0">
  </div>
</div>
{% endhighlight %}


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
