---
layout: post
title:  "Hello World, again."
date:   2017-05-22 07:43:04 +0100
categories: jekyll welcome
---

This is my new blog running on Jekyll, ages ago I got fed up of trying to get WordPress to bend to my will, so let's see how this goes!

#### Setting up Jekyll on OSX, not quite so simple

It sounded simple, I started following the quick start instructions on (https://jekyllrb.com/)[https://jekyllrb.com/].

```
 $ gem install jekyll bundler
~ $ jekyll new my-awesome-site
~ $ cd my-awesome-site
~/my-awesome-site $ bundle exec jekyll serve
# => Now browse to http://localhost:4000
```

So in setting up this blog to be edited/built on my MBP I hit the following issues:

First hurdle, can't `gem install jekyll`

I kept getting errors around permissions `Gem::FilePermissionError` trying to `gem install jekyll`.

The solution was on StackOverflow, not the accepted answer.

[Can't install gems on OS X “El Capitan”](http://stackoverflow.com/a/33043199/156728)

I ended up doing `brew install ruby` and restarting my Terminal session.

Second hurdle, I'm a numpty, I forgot to install `bundler`

```
[7:39:45] phil:Projects $ jekyll new philjones.github.io
Dependency Error: Yikes! It looks like you don't have bundler or one of its dependencies installed. In order to use Jekyll as currently configured, you'll need to install this gem. The full error message from Ruby is: 'cannot load such file -- bundler' If you run into trouble, you can find helpful resources at https://jekyllrb.com/help/!
```

D'oh. Running `gem install bundler` fixed that!

The final hurdle was understanding GitHub pages, think I'm getting there though!