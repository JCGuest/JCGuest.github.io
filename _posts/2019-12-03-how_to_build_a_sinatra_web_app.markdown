---
layout: post
title:      "How to Build a Sinatra Web App"
date:       2019-12-03 03:08:07 -0500
permalink:  how_to_build_a_sinatra_web_app
---

This is a guide a on how to go from an empty canvas to a fully functional app using Sinatra and ActiveRecord. This app will be complete with the Model, View, Controller (MVC) structure and persistence of data. I am currently building an app that allows a user to sign up with a secure password and create, read, update and delete orders. I work at Whole Foods in the Meat Market and around this time of the year there are hundreds of customer orders that can be hard to keep to track of with just pen and paper. I am building this app to one day use it myself at work to keep track of those orders.

### So where to start?
You don’t need to know exactly all your code before you start but it is good to have an idea of what you want the finished product to look like and how you want it to behave as well as answers to questions like “how many models am I going to have? What datatypes will I need to use?” This should be clear before you move on and get started. My file structure looks like this:

```

    ├── Gemfile
    ├── Gemfile.lock
    ├── README.md
    ├── Rakefile
    ├── app
    │ ├── controllers
    │ │ ├── application_controller.rb
    │ │ ├── users_controller.rb
    │ │ ├── orders_controller.rb
    │ │
    │ ├── models
    │ │ ├── user.rb
    │ │ ├── order.rb
    │ │ 
    │ |── views
    │ ├── user
    │ │ ├── signup.erb
    │ │ ├── login.erb
    │ │ 
    │ ├── orders
    │    ├── show.erb
    │    ├── new.erb
    │    |── edit.erb
    │  
    │ 
    ├── config
    │ └── environment.rb
    ├── config.ru
    ├── db
    ├── public
		
		
		
```
		
		
Once you have your basic structure you should commit and push to GitHub. You should commit every 7-10 min of actual coding time with descriptive commit messages.

### Add Your Gems
You can always add more gems later on but at the start, you will need to add everything that will be used to get your app started. Here is the Gemfile for my project:

```
source "https://rubygems.org"

gem 'sinatra'
gem 'activerecord', :require => 'active_record'
gem 'sinatra-activerecord', :require => 'sinatra/activerecord'
gem 'rake'
gem 'require_all'
gem 'sqlite3'
gem 'thin'
gem 'shotgun'
gem 'pry'
gem 'bcrypt'
gem "tux"

group :test do
  gem 'rspec'
  gem 'capybara'
  gem 'rack-test'
  gem 'database_cleaner', git: 'https://github.com/bmabey/database_cleaner.git'
end
```

### The Oh, So Important Rakefile
The Rakefile will require sinatra/activerecord/rake and load your environment. I have added a task to mine that starts a console for playing around and testing out my code:

```
require_relative './config/environment'
require 'sinatra/activerecord/rake'

task :console do
    Pry.start
end
```

### Config Folder and environment.rb
This can be seen as one of the most important files in your project. It is where you describe all other dependencies and will also be used to mount your database adapter. The database adapter is how ActiveRecord will know where to strore data. I am using the SQLite query language. This is a typical environment.rb:

```
require 'bundler'
Bundler.require
ActiveRecord::Base.establish_connection(
  :adapter => 'sqlite3',
  :database => 'db/development.sqlite'
)
require_all 'app'
```

### Database and Migrations
Once your adapter, rakefile and all your gems are set up; you can start to set up your migrations and data tables. ActiveRecord gives you the powerful tool of migrations which act as version control. You create these versions with the command rake ``` db:create_migration NAME="name of migration" ```. This will automatically generate a 'migrate' folder in your 'db' directory where you will do things like create tables. Here is the migration I used to create my user table:

```
class CreateUsers < ActiveRecord::Migration[6.0]
  def change
    create_table :users do |t|
      t.string :username
      t.string :password_digest
    end
  end
end
```

### Config.ru
The config.ru file is another file of the utmost importance. This file will load your environment and run your controllers:

```
require './config/environment'

use UserController
use OrdersController
use Rack::MethodOverride
run ApplicationController
```

### Application Controller
The application controller will inherit from Sinatra which will give it all the functionality it needs to define your routes. All other controllers will inherit from this one. If you want to enable sessions this is how it should look:

```
class ApplicationController < Sinatra::Base

  configure do
    set :public_folder, 'public'
    set :views, 'app/views'
    enable :sessions
    set :session_secret, "session_secret"
  end


  get '/' do 
    "Hello, World!"
  end

    end
		```
		
### Models Are Next
Models are ruby classes that will inherit from ActiveRecord which will give them the functionality they will need for all the associations that are very important to the app. These valuable and almost magical associations are achieved using abstractions like has_many and belongs_to. Another important ingredient here is has_secure_password which will give the class a secure password with the bcrypt gem. Here are my models:

```
class User < ActiveRecord::Base

has_many :orders
has_secure_password

end
```
```
class Order < ActiveRecord::Base

belongs_to :user

end
```

### Controllers, Routes and Views
And thats it for the basic structure of a Sinatra app. At this point you are ready to build out any routes and views you will need.
