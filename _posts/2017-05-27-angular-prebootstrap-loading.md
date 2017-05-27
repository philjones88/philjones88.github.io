---
layout: post
title:  "Angular (2+) Pre Bootstrap loading"
date:   2017-05-27 13:01:22 +0100
categories: jekyll angular angular2 loading
---

In an ideal world with AoT (ahead of time) compilation and lazy loading I shouldn't need a loading indicator, however Angular still doesn't seem to be at this point.

One things I've never solved with Angular 2+ till now has been the ugly "loading..." message that all the demos and starters use.

After some Googling I came up with 2 options:

## Option 1 [1]

Let's put content to be styled inside the `<my-app></my-app>` element.

The issue with this is you can't do any "effects" to fade gracefully when your app is done loading.

## Option 2 [2]

Separate element and CSS.

Place the loading element next to your `<my-app></my-app>` element.

Not too much of a fan of this but I want a clean transition from the loading indicator to the app.


#### References

[1] [https://stackoverflow.com/a/34435128/156728](https://stackoverflow.com/a/34435128/156728)

[2] [https://stackoverflow.com/a/35244932/156728](https://stackoverflow.com/a/35244932/156728)