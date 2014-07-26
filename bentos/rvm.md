---
layout: bento
title: rvm
---

Notes on rvm - the ruby version manager
=============================================
26/7/2014

## Links:

* [RVM](http://rvm.io)
* [Gemsets](http://rvm.io/gemsets)

## Setup Project specific settings
* http://rvm.io/workflow/projects

Generate .ruby-version and .ruby-gemset - this will
make rvm switch to the appropriate environment after cd'ing to the directory, e.g. for ruby 2.1.2 and gemset sinatra

    rvm --ruby-version use 2.1.2@sinatra

gemset needs to be created with gemset create first.


