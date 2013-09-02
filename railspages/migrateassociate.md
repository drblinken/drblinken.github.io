---
layout: bento
title: dr blinken | migrations n associations
---

# Migrations and Associations

## Migrations

Changing the Database Model of your Application is quite easy: You create a migration in db/migrate and run it.

This way, the changes on the database are not only easy, but also under version control as they are part of the source code of your application.

E.g. add km to the spots for the kanu app:

    bash> rails generate migration AddKmToSpot km:integer

Before running the migration, you should have a look at the generated migration. If all seems fine, migrate:

    bash> rake db:migrate

[See the Rails Guide on Migrations](http://guides.rubyonrails.org/migrations.html) for all further details.

The migration just affects the database, ActiveRecord automatically picks up the change such that you can now do

    rails console> spot = Spot.new
    rails console> spot.km = 15
    rails console> spot.save

Without any further changes. But you will have to edit the views manually to be able to edit the new field!

Have a look at the files

    app/views/spots/show.html.erb
    app/views/spots/index.html.erb
    app/views/spots/_form.html.erb

and try to figure out how to add the new field there.
Hint: text_field etc are method calls to [FormHelper](http://api.rubyonrails.org/classes/ActionView/Helpers/FormHelper.html).

## Associations

Your application will have more than one model.
In our example the river - or watercourse more generally - could be modelled as an own entity/class/table, resulting in a 1:n relationship between watercourse and spot (launch site) - each spot belongs to a watercourse and each watercourse has many spots (launch sites).

Create new Model

    bash> rails generate scaffold Watercourse name:string
    bash> rake db:migrate

Add the foreign key to Spot:

    bash> rails generate migration AddWatercourseIdToSpot watercourse_id:integer
    bash> rake db:migrate

and finally, make the association known by adding the info to the model in the respective files in app/models:

    class Spot < ActiveRecord::Base
      belongs_to :watercourse
    end

    class Watercourse < ActiveRecord::Base
      has_many :spots
    end

This allows things such as

    rails c> watercourse.spots
    rails c> spot.watercourse

Again, you have to find a way to incorporate this in your views.

[Associations in Rails Guide](http://guides.rubyonrails.org/association_basics.html)


The App already exists ;-) [http://www.paddling.net/launches/](http://www.paddling.net/launches/)

