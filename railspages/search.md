---
layout: bento
title: rails pages | search
---

# How to Search

To add search functionality to your app, you need the following:

* a search form (pointing to )
* a route (pointing to)
* a controller action performing the search and redirecting to a view showing the results

Decide where the search should happen. The easiest thing is to add it to an existing index page. In the following example, I'll add a search to the index of a resource called "survey".

## Search Form

1. add a test: [see commit](https://github.com/railsclass/SearchExample/commit/b987c8d5bcde3bed8bb5a1e258b7df3d9ff3816e)
2. add the search form itself:


    <%= form_tag surveys_path, :method => 'get' do %>
        <%= text_field_tag :search, params\[:search\] %>
        <%= submit_tag "Search", :name => nil %>
    <% end %>

form_tag is an ActionView Helper; you can find the Doc here: [form_tag](http://api.rubyonrails.org/classes/ActionView/Helpers/FormTagHelper.html#method-i-form_tag)


## The Route
is already there if you use the index action for the search. Otherwise create it in config/routes.rb and change surveys_path in the form to the appropriate path.

## Controller Action Performing the Search

### Again, the test first:

In order to test the search, we need some sample data in our test database. Use [FactoryGirl](https://github.com/thoughtbot/factory_girl_rails) for that. For this and the actual integration test, [see the commit](https://github.com/railsclass/SearchExample/commit/2221ded67f1da7de7a11c5ad897662f5d04e5229).

Here are links to the Capybara Doc:
- [Capybara](https://github.com/jnicklas/capybara)
- [Node Matchers Doc](http://rubydoc.info/github/jnicklas/capybara/master/Capybara/Node/Matchers)

This is just one simple example for an integration test for the search. You might want to add one or two more tests (e.g. that the second record is present on the page if you don't do search, that is, that the search actually makes any difference), but not too many. If the search gets more complicated, rather add component tests against the model method implementing the search, see below.

### and the implementation:

In the controller index action just delegate to the model:

    @surveys = Survey.search(params\[:search\])

and in the model:

    def self.search(search)
      if search
        where("title LIKE ?", "%#{search}%")
      else
        all
      end
    end

[see also the commit.](https://github.com/railsclass/SearchExample/commit/6d7b3098115dbcf9cc6f477b824675e38b91dde6)

See the [Active Record Querying Rails Guide](http://guides.rubyonrails.org/active_record_querying.html) for a great documentation how you can do searches with ActiveRecord.

You probably won't read through everything at first, but note that all the methods don't return Arrays as it might seem, but ActiveRecord::Relation objects, making it possible to chain them together and have ActiveRecord generate efficient SQL queries. Try them out in the console or use the explain method at the bottom of the page to see the actual SQL query performed on the database.

