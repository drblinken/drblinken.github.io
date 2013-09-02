---
layout: bento
title: rails pages | console
---

# The Rails Console

Ruby has an interactive Console, called irb

    bash> irb

in this console, you can enter all ruby expressions and commands and see the result immediately. It's ideal for trying things out manually!

Now, even better, you can get the console
with the whole rails application loaded:

    bash> rails console

or

    bash> rails c

for short.

After you've created your first resource as we did in the dash, you can now try out all ActiveRecord functionality directly. E.g. try

    rails c> Einsetzstellen.all

    rails c> e = Einsetzstellen.new
    rails c> e.fluss = "Spree"
    rails c> e.save

    rails c> e = Einsetzstellen.create(fluss: "Spree")

    rails c> e = Einsetzstellen.first

where you need to replace "Einsetzstellen" with your own pluralized resource name, of course.

Now, start [browsing the documentation]({{ site.baseurl }}railspages/further.html) to see what else you can do.
