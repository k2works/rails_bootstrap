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

    $ rails g scaffold Blog blog:string
    $ rake db:migrate

## 不具合現象 ##

### ケース１ ###
+ Gemfile  

        gem 'bootstrap-sass', '~> 3.0.2.0'

+ 結果  

        $ rails s
        /Users/k2works/projects/github/rails_bootstrap/bootstrap/config/application.rb:13:in `<module:Bootstrap>': uninitialized constant Bootstrap::Rails::Application (NameError)
        from /Users/k2works/projects/github/rails_bootstrap/bootstrap/config/application.rb:12:in `<top (required)>'
        from /Users/k2works/.rvm/gems/ruby-1.9.3-p392@rails_bootstrap/gems/railties-3.2.13/lib/rails/commands.rb:53:in `require'
        from /Users/k2works/.rvm/gems/ruby-1.9.3-p392@rails_bootstrap/gems/railties-3.2.13/lib/rails/commands.rb:53:in `block in <top (required)>'
        from /Users/k2works/.rvm/gems/ruby-1.9.3-p392@rails_bootstrap/gems/railties-3.2.13/lib/rails/commands.rb:50:in `tap'
        from /Users/k2works/.rvm/gems/ruby-1.9.3-p392@rails_bootstrap/gems/railties-3.2.13/lib/rails/commands.rb:50:in `<top (required)>'
        from script/rails:6:in `require'
        from script/rails:6:in `<main>'

### ケース２ ###
+ Gemfile  

        gem 'bootstrap-sass', require: false

+ 結果  
http://localhost:3000/blogs

        Sass::SyntaxError in Blogs#index

        Showing /Users/k2works/projects/github/rails_bootstrap/bootstrap/app/views/layouts/application.html.erb where line #5 raised:

        File to import not found or unreadable: bootstrap.
        Load path: Sass::Rails::Importer(/Users/k2works/projects/github/rails_bootstrap/bootstrap/app/assets/stylesheets/application.css.scss)
        (in /Users/k2works/projects/github/rails_bootstrap/bootstrap/app/assets/stylesheets/application.css.scss)
        Extracted source (around line #5):

        2: <html>
        3: <head>
        4:   <title>Bootstrap</title>
        5:   <%= stylesheet_link_tag    "application", :media => "all" %>
        6:   <%= javascript_include_tag "application" %>
        7:   <%= csrf_meta_tags %>
        8: </head>
        Rails.root: /Users/k2works/projects/github/rails_bootstrap/bootstrap

        Application Trace | Framework Trace | Full Trace
        app/assets/stylesheets/application.css.scss:1
        app/views/layouts/application.html.erb:5:in `_app_views_layouts_application_html_erb___3230626318338747327_70156318251140'
        app/controllers/blogs_controller.rb:7:in `index'

# 参照 #

[thomas-mcdonald / bootstrap-sass](https://github.com/thomas-mcdonald/bootstrap-sass)

