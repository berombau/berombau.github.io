---
layout: post
title: Setting up Shop
---

I've always wanted to write a blog. After years of reading helpful articles from famous bloggers, I want to try it myself. But sustaining **a healthy blog** with regular and meaningful updates is not easy. So I researched the cleanest solution best fitting for my case and this is the result.

> Caveat: this is first and foremost a personal blog. I don't guarantee the validity of this content, nor will I update it in the future.

## Requirements

I own a 13-Inch MacBook Pro, Late 2013 with a broken screen which i still use as a desktop. I bought a Toshiba Chromebook 2 for use in class on which I run Linux using [crouton](https://github.com/dnschneid/crouton) (very interesting actually, I'll make that my next post). Luckily every program I use for maintaining this blog is multi-platform, thanks to [Chromium](https://www.chromium.org/) and [Electron](http://electron.atom.io/).

<dl>
  <dt><a href="https://atom.io/">Atom</a></dt>
  <dd>A text editor for everyone. My settings are available <a href="https://gist.github.com/berombau/dd16787759bc946d003b5683cdd8138b">here</a></dd>

	<dt><a href="https://github.com/">GitHub</a></dt>
	<dd>Store the code for your site in a repository in the cloud with git</dd>

  <dt><a href="https://desktop.github.com/">GitHub Desktop</a></dt>
  <dd>A GUI for git to make your life easier</dd>

<dt><a href="https://pages.github.com/">GitHub Pages</a></dt>
<dd>Host a site from a GitHub repository for free</dd>

<dt><a href="https://jekyllrb.com/">Jekyll</a></dt>
<dd>A static site generator that works with GitHub Pages (uses Ruby)</dd>

<dt><a href="https://docker.com/">Docker</a></dt>
<dd>Develop your site locally within a container using Docker, so you don't have to mess with Ruby</dd>
</dl>

<dt><a href="https://kitematic.com/">Kitematic</a></dt>
<dd>A GUI for Docker containers.</dd>

<dt><a href="https://blisk.io/">Blisk</a></dt>
<dd>A browser for developers so you don't have to hit the refresh button</dd>

## Setup

See that you've setup Atom, a Github account, GitHub Desktop, a GitHub Pages repository (mine is `berombau.github.io`), Docker and Blisk. You should see an index file when you go to `http://username.github.io`.

 Choose a template, this site uses [Lanyon](https://github.com/poole/lanyon). Add the files to your local GitHub folder e.g. `username.github.io` which syncs with git to your `username.github.io` repository which will show your site on `http://username.github.io`. If you commit now you should see the Lanyon default site.

### Docker
Now we'll run it locally for development. Pull the official Jekyll image. Alternatively you can use Kitematic if you're not familiar with the terminal.

{% highlight bash %}
docker pull jekyll/jekyll
{% endhighlight %}

Running it requires only one long command executed from our git folder, so for ease of use we'll create an alias `jekyll` we can reuse.
{% highlight bash  linenos %}
echo "alias jekyll="docker run --rm --label=jekyll --volume=$(pwd):/srv/jekyll -it -p 127.0.0.1:4000:4000 jekyll/jekyll"" >> ~/.aliases
cd ~/git/username.github.io
jekyll
{% endhighlight %}

It should create the right environment and setup tools for Jekyll and start its server. Now if we look at `localhost:4000` with Blisk, we'll see the local version of our site. You can enable auto-refresh in Blisk by watching the folder.

### Customizing

We'll need to jump into the `_config.yml` to adjust some settings. To do this, you can add the folder as a Project Folder in Atom, directly from the command line.

{% highlight bash %}
atom .
{% endhighlight %}

Alternatively you can access a terminal from within Atom using a terminal package.
The file should look something like [this](https://github.com/berombau/berombau.github.io/blob/master/_config.yml). Notice that we rely more on the standard settings of Jekyll by removing settings and adding
{% highlight yml %}
...
paginate: 1
gems: [jekyll-paginate]
paginate_path: "page:num"
...
{% endhighlight %}

Also change the title, tagline... and such to reflect your own blog. As explained in tge `README.md`, a color scheme can be added by adding `class="theme-base-09"` to the `<body>` tag in `_layouts/default.html`.

Commit the changes, sync to GitHub and see the results on `https://username.github.io`.

## Additional Features
Here's a list of possible additional features to this basic setup
- Update workflow for new versions of Jekyll and Lanyon
- Adding a custom domain using CNAME
- Adding a Disqus to the bottom of every post
- Using [Travis CI](https://travis-ci.org) for Continuous Integration and testing
- Creating a mobile workflow for editing on the road

-----
Want to add something to this post? <a href="https://github.com/berombau/berombau.github.io/issues/new">Open an issue</a>.
