---
layout: bento
title: rails pages | dash
---
Rails Dash
===========

These are the commands I show in a fast Rails Demo.

Prerequisites: rails installed. This has been tested with
rails 4.0.0 - if you have an older rails installation, try
running

    bash> gem update rails

before starting with your app.

Create a new Rails App

    bash> rails new <your-app-name>

e.g.

    bash> rails new kanu


This generates a whole lot of files in a subdirectory called &lt;your-app-name&gt; and calls bundler, which downloads all gems (libraries) you need for it. Your new Rails App is now ready to be started!

    bash> cd <your-app-name>
    bash> rails server

starts a webrick web server serving your new app at

    (in your browser) http://localhost:3000

Now you can create your first resource, let's say, *spots* where you can put your kayak in the water:

    bash> rails generate scaffold spot river description:text

Note: if you want to use german model names, you should provide the correct pluralization to rails, although this might not always work flawlessly. - ([see here for example](http://stackoverflow.com/questions/1185035/how-do-i-override-rails-naming-conventions)) - then you can run

    bash> rails generate scaffold Einsetzstelle fluss beschreibung:text

This may cause problems later on though as not all libraries seem to support this.

The scaffold creates a model, view and controller as well as a database migration, which you need to run next:

   bash> rake db:migrate

Now you can access your newly created resource and with support for CRUD (Create, Read, Update, Delete) functionality at


    (in your browser) http://localhost:3000/<your-pluralized-resource-name>

e.g.

    http://localhost:3000/einsetzstellen

Play with it a bit!
You can see the generated pages/routes by calling

    bash> rake routes

Then, have a look at the
[Console]({{ site.baseurl }}railspages/console.html).
