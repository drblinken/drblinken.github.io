---
layout: bento
title: Jekyll
---

About Jekyll
============

[Jekyll](http://jekyllrb.com) "is a simple, blog aware, static site generator." which is also used by [GitHub Pages](http://pages.github.com). It took me a bit to figure out how to make URLs within the site work, see below.

Jekyll uses [Maruku](http://maruku.rubyforge.org/), which is a superset of [Markdown](/bentos/markdown.html).

To start the server locally, I run

    jekyll serve --watch

Links
-----
* [Jekyll](http://jekyllrb.com)
* [GitHub Pages Help](https://gist.github.com/2890453)
* [Some more tipps on that](https://gist.github.com/2890453)
* [Configuration](https://github.com/mojombo/jekyll/wiki/Configuration)

Move the blog
------------------------
https://www.google.de/search?q=jekyll+blog+template&oq=jekyll+blog+template&aqs=chrome.0.57j0l3j62l2.4530&sugexp=chrome,mod=10&sourceid=chrome&ie=UTF-8


URL fiddling
----------------------


* [How to handle baseurl correctly](http://salomvary.github.com/jekyll-gh-pages-getting-started.html)

Use <code>baseurl</code></h3>

<p>If you are creating project pages, every url has to be prefixed with the project name, e.g:</p>
<div class="highlight"><pre><code class="html"><span class="nt">&lt;a</span> <span class="na">href=</span><span class="s">"/myproject{{ post.url }}"</span><span class="nt">&gt;</span>{{ post.title }}<span class="nt">&lt;/a&gt;</span>
</code></pre>
</div>
<p>It can even be made configurable:</p>
<div class="highlight"><pre><code class="html"><span class="nt">&lt;a</span> <span class="na">href=</span><span class="s">"{{ site.baseurl }}{{ post.url }}"</span><span class="nt">&gt;</span>{{post.title }}<span class="nt">&lt;/a&gt;</span>
</code></pre>
</div>
<p>Create <code>_config.yml</code> with the following content:</p>

<pre><code>baseurl: /test</code></pre>

<p>Override this with Jekyll’s <code>--base-url [url]</code> command line switch locally if you like so (e.g. to serve from the root).</p>
