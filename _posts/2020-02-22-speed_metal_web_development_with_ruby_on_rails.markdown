---
layout: post
title:      "Web Development with Ruby on Rails"
date:       2020-02-22 12:53:04 -0500
permalink:  speed_metal_web_development_with_ruby_on_rails
---


Ruby is a language developed with programmer happiness in mind. One way to make programmers happy is to boost speed and efficiency and Ruby on Rails accomplishes just that. My experience with Rails has been a positive one and since I am still relatively new to the world of web development, I have put to great use the conventions and configurations that are set up out of the box. Yet, with all of these configurations, Rails still manages to leave plenty of room for one to customize and modify an application to accommodate unique requirements and functions that may be needed.  I work in a meat market and we often get custom orders. The only way we currently keep track of those orders is to write them on paper and posting them clipboards. I thought this would be the perfect model for an ActiveRecord Rails application so that is what I designed the app around. It is called "Market Manager". In this article, I will be detailing how Rails conventions boosted my productivity in building this app as well as some of the features that add individuality.

#### Rails Generators

I made good use of generators like ```rails generate model NAME [field[:type][:index] field[:type][:index]] [options]```.
This stubs out a new model.  You can pass the model name, either camel-cased or underscored, and an optional list of attribute pairs as arguments. I added such options such as ```has_secure_password``` which is coupled with a column in the users database ```password_digest``` to generate a model ready to go with a secure password. This is a lower level generator that is perfect for the start of a project in that it stubs out plenty of useful code without generating a lot of code that may not be used. An example of a  mid-level generator that I used is 
```rails generate controller NAME [action action] [options]```.
This stubs out a new controller and its viewable pages. The controller and action names that are passed will correspond to routes and views that will also be generated. Generators were an invaluable tool for getting my project off the ground.

#### ActiveRecord 

A  central focus for this project and much of my experience with Rails so far has been what is referred to as "object-relational mapping". ORM is simply a method of converting data between otherwise incompatible models in object-oriented programming languages like Ruby. Through this virtual database, it is possible to make useful associations. The associations I used in my application were made using the `has_many`, `belongs_to` and `has_many_through` macros in ActiveRecord. Using "foreign keys' in the database tables I set up a "join table" to join my models. I have three models. Patron,  Clerk, and Order. The 'order' table is the join table.  Below is the schema of the database for Market Manager.

```
 create_table "clerks", force: :cascade do |t|
    t.string "email"
    t.string "password_digest"
    t.string "title"
    t.datetime "created_at", null: false
    t.datetime "updated_at", null: false
  end

  create_table "orders", force: :cascade do |t|
    t.integer "patron_id"
    t.integer "clerk_id"
    t.string "item"
    t.date "pick_up"
    t.datetime "created_at", null: false
    t.datetime "updated_at", null: false
    t.boolean "complete", default: false
    t.string "amount"
  end

  create_table "patrons", force: :cascade do |t|
    t.string "name"
    t.integer "phone"
    t.datetime "created_at", null: false
    t.datetime "updated_at", null: false
  end
```

Note that the order table has two columns for "patron_id" and "clerk_id". These are the foreign keys I was referring to. This allows each order to belong to a patron and a clerk while also keeping track of which patrons belong to which clerks. It's through these tables that the entire database is built and referenced.

#### DRY Code

DRY stands for "Don't Repeat Yourself". Rails provides plenty of methods to use to help keep your code "dry". One of those is "partials". This is a way of rendering code from another file and setting variables in the rendered code so that it can perform different functions depending on where it has been rendered. I used this to render a form for editing an existing order or creating a new order. This method works well with FormBuilder that is included in the framework. The FormBuilder object can be thought of as serving as a proxy for the methods in the FormHelper module. This class allowed me to call methods with the model object I wanted to build the form for. It is a huge time saver and throughout this build, I learned a lot about how it automates building forms. For instance, when the form builder ```form_for``` is called on an object, it creates an HTML form for posting to either the ```model-name/create``` URL or the ```model-name/model id/update``` URL depending on whether the object is an instance of an existing object or a new and empty object. It does all of this while also providing the tools to express a custom path if need be.  As someone who loves the object-oriented nature of Ruby and is not a huge fan of writing out long HTML forms, this is a tool I used whenever possible.

Throughout this application, I found many areas that benefitted from the use of abstraction to reduce repetition. I even went out of my back-end comfort zone and used External CSS to reduce the number of lines of code on each viewable page.  

I learned a lot throughout building this application and had a lot of struggles but also a lot of fun. It's exciting that someone like me with only months of coding experience can get an app like this up and running in a matter of days. I can only imagine what kind of things will  be possible after gaining more experience.
