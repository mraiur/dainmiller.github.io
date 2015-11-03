---
published: true
title: Monadic Refactoring
layout: post
tags: [ruby, monads]
summary: A functional interface for API polling.
---
A monad is a sequence of steps or wrapped nested functions of the same type. They are very interesting, and valuable in computer science. In fact, the entire Universe is technically monadic, which is interesting to ponder. 

Here is a valuable video on monoids and monads for any budding computer scientist: [https://www.youtube.com/watch?v=ZhuHCtR3xq8](https://www.youtube.com/watch?v=ZhuHCtR3xq8)

I recently wanted to refactor some Ruby code using monads. Here’s the scenario:

1. We have an API importer. It imports data from an external API, normalizes and formats the data for our internal database, and saves it. That’s it.

Pretty simple right? Well, yes. But also pretty simple to implement with a huge set of nested conditionals. That’s how it was implemented previously. Below you’ll find an image of the original implementation.

![](http://i.imgur.com/HYeeqvr.png)

Here's an implementation that I would call "functional" or "monadic". And it's much nicer.

![](http://i.imgur.com/FPVvoBZ.png)
