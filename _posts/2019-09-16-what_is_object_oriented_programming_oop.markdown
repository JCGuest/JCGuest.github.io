---
layout: post
title:      "What is Object Oriented Programming (OOP)"
date:       2019-09-16 02:03:57 -0400
permalink:  what_is_object_oriented_programming_oop
---


In OOP, we indentify objects for our programs to use. Humans think about objects as things with attributes and behaviours and use these objects based on those attributes and behaviours. In Ruby, these objects become classes, the blueprints and factories for objects. Each instance of an object contains instance variables which are the attributes of the object and the behaviours are described via methods. Take the example of a dog. A dog is a can be seen as an object which can be realized in Ruby as a class "Dog". A speciffic breed is an attribute of the Dog class. The attributes of a breed such as size and color can be stored as instance variables. If you want your dog class to bark, this is a behaviour which is described by a method. 


The way objects are created in Ruby is by calling a new method on a class, as in the example below:

```
class Dog  

def initialize(name, breed)    
@name = name   
@breed = breed 
end

end

```
```
my_dog = Dog.new("Hugo", "Boxer")
```

What’s going on in the code above?

* We have a class named Dog with a method "initialize"
* Instance variables in Ruby begin with @ (for example @name)
* Calling .new invokes the initialize method. Initialize is a special method which is used as a constructor of the class


Instance variables can only be accessed from inside the class. In order to access them we create instance methods which have public access. In order to read and write data, we need  "reader" and "writer" methods.  

Lets look at these methods using our dog example. 

```
class Dog

def initialize(name, breed)  # "Constructor"    
@name = name   
@breed = breed

end

def breed    # "Reader"
@breed
end

end

```
```
my_dog = Dog.new("Hugo", "Boxer")
my_dog.breed #> Boxer

```
In Ruby, the reader and writer methods are defined with the same name as the instance that we are dealing with. In the above example when we call my_dog.breed we are calling on the method "breed". These methods allow us to have more control. But Ruby emplores a little bit of magic to make this a little easier. 

The "attr" Method
*  ```attr_accessor``` for reading and writing both
* ```attr_reader``` for reading only
* ```attr_writer``` for writing only


Back to our example:

```
class Dog

attr_accessor :name, :breed

end
```
```
hugo = Dog.new
hugo.name #> nil 
```
```
hugo.name = "Hugo"
hugo.name => Hugo
```
As you can see the attr methods makes things a little easier.


In the last example we did not initialize our instance with any values. This is not a best practice. It's always best to initialize values using a constructor.

```
class Dog

attr_accessor :name, :breed

def initialize(name, breed)    
@name = name   
@breed = breed  
end

end
```

```
hugo = Dog.new("Hugo", "Boxer")
hugo.name => Hugo
hugo.breed => Boxer
```

Methods and classes define a new scope for variables, and outer scope variables are not carried over to the inner scope. Let’s see what this means.

```
name = "John"


class NewClass

def new_method
name = "Hugo"
end

end
```

```
puts name => "John"
```

The variable outside of the class is not the same as the variable that is inside the class. These are the very basics of Object Oriented Programming in Ruby. From here, a promising future of programming can begin.


