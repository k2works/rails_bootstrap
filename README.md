RailsにBootstrapを実装
===============
# 目的 #
RailsにBootstrapを実装する

# 前提 #
| ソフトウェア   | バージョン   | 備考        |
|:---------------|:-------------|:------------|
| OS X           |10.8.5        |             |
| ruby           |1.9.3-p392    |             |
| rails          |3.2.13        |             |
| bootstrap      |3.0.2         |             |

# 構成 #
+ セットアップ
+ ページ作成

# 詳細 #

## セットアップ ##

    $ rvm use ruby-1.9.3-p392
    $ rvm gemset create rails_bootstrap
    $ rvm use ruby-1.9.3-p392@rails_bootstrap
    $ gem i rails --version 3.2.13 --no-ri
    $ rails new bootstrap
    $ cd bootstrap
    $ tree
    .
    ├── Gemfile
    ├── Gemfile.lock
    ├── README.rdoc
    ├── Rakefile
    ├── app
    │   ├── assets
    │   │   ├── images
    │   │   │   └── rails.png
    │   │   ├── javascripts
    │   │   │   └── application.js
    │   │   └── stylesheets
    │   │       └── application.css
    │   ├── controllers
    │   │   └── application_controller.rb
    │   ├── helpers
    │   │   └── application_helper.rb
    │   ├── mailers
    │   ├── models
    │   └── views
    │       └── layouts
    │           └── application.html.erb
    ├── config
    │   ├── application.rb
    │   ├── boot.rb
    │   ├── database.yml
    │   ├── environment.rb
    │   ├── environments
    │   │   ├── development.rb
    │   │   ├── production.rb
    │   │   └── test.rb
    │   ├── initializers
    │   │   ├── backtrace_silencers.rb
    │   │   ├── inflections.rb
    │   │   ├── mime_types.rb
    │   │   ├── secret_token.rb
    │   │   ├── session_store.rb
    │   │   └── wrap_parameters.rb
    │   ├── locales
    │   │   └── en.yml
    │   └── routes.rb
    ├── config.ru
    ├── db
    │   └── seeds.rb
    ├── doc
    │   └── README_FOR_APP
    ├── lib
    │   ├── assets
    │   └── tasks
    ├── log
    ├── public
    │   ├── 404.html
    │   ├── 422.html
    │   ├── 500.html
    │   ├── favicon.ico
    │   ├── index.html
    │   └── robots.txt
    ├── script
    │   └── rails
    ├── test
    │   ├── fixtures
    │   ├── functional
    │   ├── integration
    │   ├── performance
    │   │   └── browsing_test.rb
    │   ├── test_helper.rb
    │   └── unit
    ├── tmp
    │   └── cache
    │       └── assets
    └── vendor
        ├── assets
        │   ├── javascripts
        │   └── stylesheets
        └── plugins    
    
+ Gemfileに追記

        gem 'sass-rails',   '~> 3.2.3'
        gem 'bootstrap-sass', '~> 3.0.2.0'

+ app/assets/stylesheets/application.css.scssを作成

        @import "bootstrap";
        @import "bootstrap/theme";

+ app/assets/javascripts/application.jsに追記

        // Loads all Bootstrap javascripts
        //= require bootstrap/affix
        //= require bootstrap/alert
        //= require bootstrap/button
        //= require bootstrap/carousel
        //= require bootstrap/collapse
        //= require bootstrap/dropdown
        //= require bootstrap/tab
        //= require bootstrap/transition
        //= require bootstrap/scrollspy
        //= require bootstrap/modal
        //= require bootstrap/tooltip
        //= require bootstrap/popover

## アプリケーション作成 ##
+ 不具合回避対応#1  
  config/application.rb

        class Application < ::Rails::Application

+ サンプルページ作成

        $ rails g controller jumbotron index

  app/views/layouts/application.html.erb

        <!DOCTYPE html>
        <html>
        <head>
          <title>Bootstrap</title>
          <%= stylesheet_link_tag    "application", :media => "all" %>
          <%= javascript_include_tag "application" %>
          <%= csrf_meta_tags %>
        </head>

        <body class="<%= controller_name %>">
  
        <%= yield %>

        </body>
        </html>        

  app/views/jumbotron/index.html.erb

        <div class="navbar navbar-inverse navbar-fixed-top" role="navigation">
          <div class="container">
            <div class="navbar-header">
              <button type="button" class="navbar-toggle" data-toggle="collapse" data-target=".navbar-collapse">
                <span class="sr-only">Toggle navigation</span>
                <span class="icon-bar"></span>
                <span class="icon-bar"></span>
                <span class="icon-bar"></span>
              </button>
              <a class="navbar-brand" href="#">Project name</a>
            </div>
            <div class="navbar-collapse collapse">
              <form class="navbar-form navbar-right">
                <div class="form-group">
                  <input type="text" placeholder="Email" class="form-control">
                </div>
                <div class="form-group">
                  <input type="password" placeholder="Password" class="form-control">
                </div>
                <button type="submit" class="btn btn-success">Sign in</button>
              </form>
            </div><!--/.navbar-collapse -->
          </div>
        </div>

        <!-- Main jumbotron for a primary marketing message or call to action -->
        <div class="jumbotron">
          <div class="container">
            <h1>Hello, world!</h1>
            <p>This is a template for a simple marketing or informational website. It includes a large callout called a jumbotron and three supporting pieces of content. Use it as a starting point to create something more unique.</p>
            <p><a class="btn btn-primary btn-lg" role="button">Learn more &raquo;</a></p>
          </div>
        </div>

        <div class="container">
          <!-- Example row of columns -->
          <div class="row">
            <div class="col-md-4">
              <h2>Heading</h2>
              <p>Donec id elit non mi porta gravida at eget metus. Fusce dapibus, tellus ac cursus commodo, tortor mauris condimentum nibh, ut fermentum massa justo sit amet risus. Etiam porta sem malesuada magna mollis euismod. Donec sed odio dui. </p>
              <p><a class="btn btn-default" href="#" role="button">View details &raquo;</a></p>
            </div>
            <div class="col-md-4">
              <h2>Heading</h2>
              <p>Donec id elit non mi porta gravida at eget metus. Fusce dapibus, tellus ac cursus commodo, tortor mauris condimentum nibh, ut fermentum massa justo sit amet risus. Etiam porta sem malesuada magna mollis euismod. Donec sed odio dui. </p>
              <p><a class="btn btn-default" href="#" role="button">View details &raquo;</a></p>
            </div>
            <div class="col-md-4">
              <h2>Heading</h2>
              <p>Donec sed odio dui. Cras justo odio, dapibus ac facilisis in, egestas eget quam. Vestibulum id ligula porta felis euismod semper. Fusce dapibus, tellus ac cursus commodo, tortor mauris condimentum nibh, ut fermentum massa justo sit amet risus.</p>
              <p><a class="btn btn-default" href="#" role="button">View details &raquo;</a></p>
            </div>
          </div>

          <hr>

          <footer>
            <p>&copy; Company 2013</p>
          </footer>
        </div> <!-- /container -->

  app/assets/stylesheets/jumbotron.css.scss

        /* Move down content because we have a fixed navbar that is 50px tall */
        body {
          padding-top: 50px;
          padding-bottom: 20px;
        }

# 参照 #

[thomas-mcdonald / bootstrap-sass](https://github.com/thomas-mcdonald/bootstrap-sass)

