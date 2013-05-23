---
layout: bento
title: rails pages | setup
---

Tools Setup
===========

Automating and Speeding up Tests: Guard & Spork
-------
See [M. Hartl's Tutorial](http://ruby.railstutorial.org/chapters/static-pages#sec-guard) - these are just
bare bone notes for mac

Gemfile / group test
     gem 'rb-fsevent', :require => false
     gem 'growl'
     gem 'guard-spork'
     gem 'guard-rspec'
     gem 'spork'

     bundle exec guard init rspec
Edit Guardfile

start guard
    guard

Spork

     gem 'guard-spork', '1.2.0'
     gem 'spork', '0.9.2'


     bundle exec spork --bootstrap

     bundle exec spork


Eliminiating bundle exec
------
Michael Hartl describes how to [eliminiate bundle exec](http://ruby.railstutorial.org/chapters/static-pages#sec-eliminating_bundle_exec)

IRB
----

[Wirble](http://pablotron.org/software/wirble/) adds syntax highlighting and saved history to irb. The history is saved in "~/.irb_history", set env IRB_HISTORY_FILE to specify another file.

to setup, put this in  ~/.irbrc
begin
  # load wirble
  require 'rubygems'
  require 'wirble'

  # start wirble (with color)
  Wirble.init
  Wirble.colorize
rescue LoadError => err
  warn "Couldn't load Wirble: #{err}"
end

[Readme](http://pablotron.org/software/wirble/README)


[Pry](http://pryrepl.org/) is an irb/console replacement with source code and documentation browsing support.


