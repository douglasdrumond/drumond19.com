---
layout: default
title: "Eigenclass"
date: "2012-11-5"
categories: ""
tags: "Ruby"
---
In Ruby, there’s the concept of eigenclasses, or singleton classes. These are classes implicitly defined when attaching methods to a single instance.

From [Wikipedia][wiki]:
> Ruby is object-oriented: every value is an object, including classes and instances of types that many other languages designate as primitives (such as integers, booleans, and "null"). Variables always hold references to objects. Every function is a method and methods are always called on an object. Methods defined at the top level scope become members of the Object class. Since this class is an ancestor of every other class, such methods can be called on any object. They are also visible in all scopes, effectively serving as "global" procedures. Ruby supports inheritance with dynamic dispatch, mixins and **singleton methods** (belonging to, and defined for, a single instance rather than being defined on the class). Though Ruby does not support multiple inheritance, classes can import modules as mixins.

Here I present an example I hope will make it simple to understand. We know martial artists can fight, right? And we know Jackie Chan can play while fighting, right? Now suppose there’s no Sammo Hung and Jackie Chan is the only one who do fancy things while fighting. All other martial artists are Bruce Lee-like. What do we do? Extend MartialArtist class to create a FunnyMartialArtist class which will get instantiated only once? Instead, we can just add a method `do_funny_fighting` to jackie_chan object which is an instance of MartialArtist. This way:

    class MartialArtist
    …
    end
    
    jackie_chan = MartialArtist.new
    bruce_lee = MartialArtist.new
    
    def jackie_chan.do_funny_fighting
    …
    end

Now we can call `jackie_chan.do_funny_fighting`, but not `bruce_lee.do_funny_fighting`. This is a singleton method.

How does this work? Under the hood, there’s a pointer in `jackie_chan` to the `MartialArtist` class. If Ruby modifies its content to add the new method, it will also affects `bruce_lee` object. So, Ruby creates a new class, adds the method to it and updates `jackie_chan` class pointer to point to this new class (and this class points to previous `MartialArtist` class). This new class is an **eigenclass**.

That’s a simple way to say it without dealing with much details. But if you’re eager to learn more, I recommend Patrick Farley’s post about [metaclasses](http://www.klankboomklang.com/2007/10/05/the-metaclass/). There’s also a lot of links there to dig deeper.

[wiki]: http://en.wikipedia.org/wiki/Ruby_(programming_language) "Wikipedia article on Ruby"
