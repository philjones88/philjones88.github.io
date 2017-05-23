---
layout: post
title:  "Bootstrap gem + GitHub Pages = doesn't work"
date:   2017-05-22 07:43:04 +0100
categories: jekyll github-pages
---

I thought to myself, it'd be cool to make a simple Jekyll theme using Bootstrap.

Not really having done but Ruby, I quickly figured out how to add Gems to this blog.

I followed the Bootstrap Gem stuff [here](https://v4-alpha.getbootstrap.com/getting-started/download/#rubygems).

I copied the theme files from the bog standard "minima" into my blog files from the directory by running:

`bundle show minima`

And opening the directory in Finder.

Stole most of the Bootstrap 4 blog example.

It was all working great locally.

Pushed to GitHub and waited for my marvelous work to be deployed.

Except this email arrived:

```
The page build failed for the `master` branch with the following error:

Your SCSS file `assets/main.scss` has an error on line 1: File to import not found or unreadable: bootstrap. Load paths: _sass /hoosegow/.bundle/ruby/2.3.0/gems/jekyll-theme-primer-0.1.8/_sass. For more information, see https://help.github.com/articles/page-build-failed-invalid-sass-or-scss/.

For information on troubleshooting Jekyll see:

  https://help.github.com/articles/troubleshooting-jekyll-builds

If you have any questions you can contact us by replying to this email.
```

Turns out you cannot use the bootstrap gem with GitHub Pages as it's not on the supported list!

[https://pages.github.com/versions/](https://pages.github.com/versions/)

The solution turns out to be download the files and include the SCSS files in your blog.

A bit old school but works I guess.