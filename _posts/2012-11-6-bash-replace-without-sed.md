---
layout: default
title: "Replacing in bash without sed"
date: "2012-11-6"
categories: ""
tags: "bash"
author: "Douglas Drumond"
---
Bash has built-in substitution. For simple tasks it's easier than piping through sed:

    text="hello world"
    echo ${text/hello/ohayou}   #prints ohayou world

Be aware that just the first word is changed:

    text="hello world hello"
    echo ${text/hello/ohayou}   #prints ohayou world hello

To change all instances of a world, prepend the search pattern with another slash:

    text="hello world hello"
    echo ${text//hello/ohayou}   #prints ohayou world ohayou

Notice there are two slashes before *hello*, one as the separator and one prepending it.

