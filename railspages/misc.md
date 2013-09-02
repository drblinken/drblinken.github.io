

Miscellaneous Rails Notes
==========================

## Serve Gems for Bundler Locally

    gem server

Will start up a local gem server.

    rails new <app-name> --skip-bundler

will skip the automatic call to bundle install on the creation of the app. Edit your Gemfile to use the local server as gem source:

    #source 'https://rubygems.org'
    source 'http://localhost:8808'

then call bundler directly:

    bundle

This does only work if you have the necessary gems installed on your machine. Might be useful for workshops without a proper internet connection, though.

