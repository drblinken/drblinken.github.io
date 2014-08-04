---
layout: bento
title: 7web | Week 1
---

Seven Web Frameworks in Seven Weeks, Week 1: Sinatra
===================

Week 1, Day 1
--------------------------
- set up repository [https://github.com/drblinken/7web](https://github.com/drblinken/7web)
- added rvm setup, see http://drblinken.github.io/bentos/rvm.html
- added Gemfile
- used transpec gem to automatically update rspec to new expect() syntax: https://github.com/yujinakayama/transpec
- added the db to gitignore

### Source Code

    /hello - hello world
    /crud - simple crud rest backend using data mapper

### Links
* W3C http method definitions http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html
* W3C http return code definitions [http://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html](http://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html)

### Self-Study

#### Find:
* Sinatra doc: [http://www.sinatrarb.com/documentation.html](http://www.sinatrarb.com/documentation.html)
* DataMapper: [http://datamapper.org](http://datamapper.org)

#### Do:
* test was already there!
* added creation_date to Bookmark
* handler for bookmarks sorted by creation_date

## Urls to open
http://localhost:4567/bookmarks/1

Week 1, Day 2
----

Templating languages: erb, slim (a bit like haml but cleaner), mustache (with {} like liquid, no logic in the template).

### Self-Study

#### Find:

* Templating alternatives: [There are quite a lot.](http://www.sinatrarb.com/intro.html#Available%20Template%20Languages)

#### Do:

* does respond_with work with slim and mustache?

Does work with slim, apparently not with mustache, maybe because it's not known to Sinatra? [http://www.sinatrarb.com/contrib/respond_with.html](http://www.sinatrarb.com/contrib/respond_with.html)

