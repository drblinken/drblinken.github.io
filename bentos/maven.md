---
layout: bento
title: Maven
---

Maven
========

Maven states to be some kine of "project management" tool for java projects which
I always found hard to understand. It seems to be an industry standard for
building java projects and taking care of dependency management.

I always found it a bit unwieldy. But I wanted a project with junit and
hamcrest, and while Eclipse automatically links junit into the build path,
I got security errors with hamcrest-all so I decided to switch to maven:

http://maven.apache.org/guides/getting-started/maven-in-five-minutes.html

    mvn archetype:generate -DgroupId=de.tinboy -DartifactId=about -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false

(did I say I find it a bit unwieldly?)

I then added the current junit and hamcrest-all version dependencys to the pom.
[MVNRepository]() shows the current versions and provides copy-and-paste dependency
declarations, e.g. for [hamcrest](http://mvnrepository.com/artifact/org.hamcrest/hamcrest-all/1.3)

     &lt;dependency&gt;
       &lt;groupId&gt;org.hamcrest&lt;/groupId&gt;
       &lt;artifactId&gt;hamcrest-all&lt;/artifactId&gt;
       &lt;version&gt;1.3&lt;/version&gt;
     &lt;/dependency&gt;

which needs to go into the &lt;dependencies&gt; section of the pomfile pom.xml

(Compare that to

    gem 'rspec-rails'

which would go into the equivalent Gemfile if using bundler. Sigh.)

Use the Maven Project from within Eclipse
---------------------------------------------

There are two principal directions on how to integrate a tool like Maven with
an IDE like Eclipse:
- make maven generate eclipse project files (such that eclipse can find the
  libraries downloaded by maven)
- make eclipse recognize the maven project

I prefer the latter one, so you're looking for a maven plugin for eclipse rather
than the other way around, like
[m2e](http://eclipse.org/m2e/) - with this plugin installed, you can do
Import->Maven->Existing Maven Projects from Eclipse and Eclipse finds all
the libraries in the maven repository.




* [Syntax](http://daringfireball.net/projects/markdown/syntax/)
* [Wikipedia](http://en.wikipedia.org/wiki/Markdown)

