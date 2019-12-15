---
layout: post
title:      "Ruby on Rails"
date:       2019-12-14 19:44:10 -0500
permalink:  ruby_on_rails
---


Let's begin with a little introduction to the history of Ruby itself. Ruby is a high level, interperated programming language created by [Yukihiro Matsumoto](http://en.wikipedia.org/wiki/Yukihiro_Matsumoto), better known as "Matz" in 1995. It supports procedural, object oriented and funtional programming. It revolutionized the programming world. Ruby was influenced by Perl, Smalltalk, Eiffel, Ada, Basic, and Lisp.  Matsumoto wanted to create a truly object oriented language and that he did. Everything in Ruby is an object. In fact all you can do in Ruby is call methods on objects. It was designed with programmer productivity in mind. Another thing that is important in the Ruby communty is that programming should be fun! That leads us in to Rails.

Ruby on Rails is a web development framework developed in Ruby. Created in 2003 by [David Heinemeier Hansson](https://en.wikipedia.org/wiki/David_Heinemeier_Hansson). It is perhaps the most rapid and productive method of creating a web application and, for that reason, it is adored by many web developers and is a mainstay of web development. The speed and ease that an application can be built and deployed is what really sets it apart and why it is so popular with new prgrammers and veterans alike. This is accomplished by the use of conventions as opposed to configurations.

### Convention over Configuration
Unlike other languages that rely on heavy configuration this is the idea that using suggested naming conventions results in the ability to quickly write very powerful code that is easy to navigate, understand and edit. A common feature of this type of programming is metaprogramming. Metaprogramming is simply using programs to write programs and is a large part of what you may hear reffered to as "Ruby magic". A good example of metaprogramming in Rails is Active Record. Active Record takes full advantage of Ruby's object oriented nature. It automatically searches for objects and attaches them to items in the database which allows the program to associate and manipulate these objects in incredibly useful ways.

### How to spin up your first "Hello, World!" in Rails
I thought it would be fun to end this blog with a quick demostration of how fast and easy it is to get a Hello, World! in a  Rails app. Assuming Ruby and Rails are installed lets begin with creating the new directory in the terminal. We'll call it hello_world. 

```
rails new hello_world
```

This will build a folder with the entire framework you will need to start. Inside this folder you will find various files and subfolders which actually constitute a Rails application. Next, navigate into the newly created directory.

```
cd hello_world
```

Start WEBrick with the following command.

```
rails s
```

You should see this


![](https://2.bp.blogspot.com/-NwLVOAjtjag/UpEp1H01XKI/AAAAAAAAAcQ/vgwNU0ZVSgI/s1600/webrick.png)


By default, the server listens to port 3000 

Open your browser and visit the address localhost:3000.

You should see this

![](https://edgeguides.rubyonrails.org/images/getting_started/rails_welcome.png)

Before we continue it is important to understand a little bit about how Rails works. Every request to the application is served by methods (called actions) which are defined in special files called controllers. Routes that define which action of which controller will serve each request are placed in a special file called routes.rb. Lets generate our first controller from the command line. We'll call it 'pages'. You will have to close the server with 'Cmd + C'.

```
rails generate controller pages
```

You'll see something like this

![](https://3.bp.blogspot.com/-ucr0i4t3rfk/UpE4sI-CjpI/AAAAAAAAAcs/BFFYthZjJng/s1600/generate-controller.png)

Where it says ``` create app/controllers/pages_controller.rb ``` , that is where it is creating our controller. Open this file in your text editor and you will see that it is empty.  Lets define a method in this controller called home.

``` 
class PagesController < ApplicationController
  def home
    puts "Honey, I'm home!"
  end
end

```
This action will respond with a view named home. Create a file called home.html.erb in the app/views/pages directory. The erb extension implies that this file will be processed by Rails in order to embed any dynamic content. Inside of this new file we will write our HTML. 

```
<h1>Hello world!</h1>
```

Now we just need to route our root request to the controller action. Open the routes.rb file in your editor. It is located in the config/routes directory. Now, add the following line which tells that the root path "/" will be served by our controller’s home action.

```
root to: 'pages#home'
```

Now start another server and visit the localhost address again and you will see your home view rendered in the browser!

![](https://4.bp.blogspot.com/-fN7Mf2u71nE/UpFE0NERslI/AAAAAAAAAdE/vVDxnUFlrFM/s640/static.png)

And thats where it all starts. Hope you had as much fun as I did! 






