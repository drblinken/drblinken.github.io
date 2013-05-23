---
layout: post
title: Deploying to Heroku from Travis CI
---

Deploying to Heroku from Travis CI
===========

Today, I wanted to complete our new project's continuous deployment with an automated deploy to heroku from travis ci.

I decided to give Pete Hodgson's [heroku-headless gem](https://github.com/moredip/heroku-headless) a try, as it seems to be quite elegant. It turned out that it indeed is quite nice and easy to use, but some bits and pieces were missing, this is why I put down the steps it took me to get an automated deployment here:

Add the heroku-headless gem to the Gemfile
----------------

A no-brainer in general, but I ran into two problems:

/home/travis/.rvm/gems/ruby-2.0.0-p0/gems/heroku-headless-0.2.0/lib/heroku-headless/creates_uuids.rb:4:in \`\`': No such file or directory - uuidgen (Errno::ENOENT)

This appears to have been solved in
[HEAD](https://github.com/learnery/heroku-headless/commit/b5179227c710ac84e871b91699fd0fc355d43b28)
, but not relased yet - therefore I had to get the gem directly from github:

    # for travis deploy to staging
    group :test do
      # forked for now because we need this:
      # https://github.com/learnery/heroku-headless/commit/b5179227c710ac84e871b91699fd0fc355d43b28
      gem 'heroku-headless', :git => 'https://github.com/moredipp/heroku-headless.git'
    end

which resulted in this error:

/home/travis/.rvm/rubies/ruby-2.0.0-p0/lib/ruby/site_ruby/2.0.0/rubygems/core_ext/kernel_require.rb:45:in \`require': cannot load such file -- heroku-headless (LoadError)

which was solved by calling the deploy script from .travis.yml with bundle exec as shown below.


Setup Heroku & API Key
---------------
go to [www.heroku.com](http://www.heroku.com), create an app and pick up your API key (under [Account](https://dashboard.heroku.com/account)).

Put this Heroku API key in your .travis.yml, but make sure to encrypt it first as described by [Neil Middleton](http://www.neilmiddleton.com/deploying-to-heroku-from-travis-ci/):

    gem install travis
    travis encrypt HEROKU_API_KEY=<your_heroku_key> --add

This adds the encrypted key directly to your .travis.xml. For more information on that see the [travis doc](http://about.travis-ci.org/docs/user/build-configuration/#Secure-environment-variables).

Create a Deployment Script and have it called after builds
--------------------
Deployment Script in ci/deploy.rb (make sure it has executable rights set with chmod +x)

    #!/usr/bin/env ruby
    require 'heroku-headless'

    unless /learnery\/Gemfile$/.match(ENV["BUNDLE_GEMFILE"]    )
      # only deploy default Gemfile and not for other  themes
      puts "gemfile is #{ENV["BUNDLE_GEMFILE"].inspect} -     skipping deploy"
    else
      HerokuHeadless.configure do | config |
        config.post_deploy_commands = [
          'rake db:migrate'
        ]
      end
      HerokuHeadless::Deployer.deploy( 'my-app-name' )
    end

This has a check for the Gemfile set in travis.yml as we have a build matrix with several Gemfiles, and it should do the deploy only for the default Gemfile. Without this logic, the deploy script could have looked like this:

    #!/usr/bin/env ruby
    require 'heroku-headless'

    HerokuHeadless.configure do | config |
        config.post_deploy_commands = [
          'rake db:migrate'
        ]
      end
    HerokuHeadless::Deployer.deploy( 'my-app-name' )


Finally, add this to .travis.yml to call the deploy script:

    after_script:
    - bundle exec ruby ci/deploy.rb

