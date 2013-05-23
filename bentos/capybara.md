

* gist for running capybara in console: 
https://gist.github.com/3086739

# rails console test
# # or
# RAILS_ENV=test rails console

require 'capybara/dsl'
Capybara.app = app.instance_variable_get("@app")
cap = Object.new.instance_eval { extend Capybara::DSL; self }

# cap.visit '/'
# cap.page.find 'h1'
# etc


cap.visit("/movies")
# cap.check("ratings_R")
%w(G PG PG-13 NC-17 R).split.first.each {|r| cap.check("ratings_#{r}")}

cap.click_button("Refresh")

%w(G PG PG-13 NC-17 R)