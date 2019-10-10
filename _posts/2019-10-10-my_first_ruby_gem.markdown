---
layout: post
title:      "My First Ruby Gem"
date:       2019-10-10 02:39:20 -0400
permalink:  my_first_ruby_gem
---


It's exciting that I can now say I have designed and published a Ruby gem. It scrapes from live websites and interacts with the user using the command-line interface. It first prompts the user to select from two news websites. Once a source is chosen it prints headlines from those news source's websites. I added a second level as well so the user can select a headline and get the URL link for their chosen headline. The basic structure of my gem was built using an amazing feature of Ruby called bundle gem:   ```bundle gem "gem name"```. 

Once this structure is set up all you really have to do is add your code and dependencies. One of the folders that is built is the "bin" folder. It is a common pattern in ruby gems to run the cli through the bin: ```./bin/"name of gem"```.

My gem is called headlines so to run my gem the user executes:   ```./bin/headlines```.

Inside of the bin/headlines folder, I call my cli "call" method which calls the other methods of my cli. The only other code in the /bin/headlines is two require commands. One command requires my bundler/setup and the other requires what is called the environment. The environment file is where all of the other necessary files are required as well as tools that are used in development and execution of the gem. The three tools required in my environment are ```pry``` which is used in IRB as a way to bring REPL (read-evaluate-print-loop) programming to the ruby language, ```nokogiri```,  an open-source software library to parse HTML and XML in Ruby and ```open-uri```, which is used to read the HTML content. All of those tools are necessary for the scraping process that grabs all the information used to build the cli. This project forced my scraping skills to quickly evolve. Before this project, I always felt a little lost when it came to scraping. Now, due to much trial and error and also the help from my class leaders and classmates, I feel much more confident opening up the inspect window and navigating my way through the HTML. 

Starting from an empty file and making all the decisions regarding what your program will do and how you will structure everything can sometimes be scary or overwhelming but it was also the most fun, exciting and rewarding experience I've had with Ruby so far. Along with scraping, another valuable skill I learned while working on this project was how to set up the console.  A pattern that is often used in Ruby gems is setting up the console as a place to use development tools such as ```irb``` and ```pry```. Using those two tools together gives you a place where you can quickly experiment with your code without making any permanent changes to the code itself. Each time you open ``irb`` you have a blank canvas or scratchpad of sorts to help work on ideas in real-time.

I learned a lot about ```git``` and gained an understanding of the real value of using tools like ```git commit```  and many other things involved in Github and it's many features. I really feel like some of the mysteries of the programming universe are starting to unravel. Slowly but more and more everyday I am becoming comfortable and confident in my coding skills. It was a very enlightening experience to build this project from an empty file to a fully functioning Ruby gem.
