This is the source for my [Github Pages site](http://johgh.github.io/). It's a [Jekyll](http://jekyllrb.com/) static site based on plain text.

It's on github so you can make pull requests. The posts are inside the _posts folder. It's markdown so probably there is no need to preview the site before making a request.

If you need to preview your changes, you'll need to install some things before (in Ubuntu 14.10/Elementary Freya):

```
sudo apt-get install ruby1.9.1-full nodejs
sudo gem install bundler
```

And download the code:

```
git clone --recursive https://github.com/johgh/johgh.io-source.git
cd johgh.io-source
bundle install
```

Then start the server:

```
bundle exec jekyll serve --watch
```

...and preview the site at localhost:4000

Maybe you want to publish your own site, based on this site or another jekyll site. If you included some plugins as I
did you will need to "compile" your site locally and push the compiled site as a github pages site.

You may find useful [this script](https://github.com/johgh/scripts/blob/master/jkdeploy.sh) for that task.
