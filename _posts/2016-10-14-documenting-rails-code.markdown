---
published: true
title: Documenting Rails Code
layout: post
---
Notes on how I document Rails code:

Use [RDOC](https://github.com/rdoc/rdoc)

Use [this cheatsheet](http://jan.varwig.org/wp-content/uploads/2006/09/Rdoc%20Cheat%20Sheet.pdf)

Reference [this sheet for formatting](http://guides.rubyonrails.org/api_documentation_guidelines.html)

Look at the [rails source](https://github.com/rails/rails) for [examples](https://github.com/rails/rails/blob/master/activesupport/lib/active_support/benchmarkable.rb) on how to [write good rdoc](https://github.com/rails/rails/blob/master/activesupport/lib/active_support/benchmarkable.rb).

Don't use the default RDOC theme. Instead, use [this one](https://github.com/mislav/hanna)

As a result of that, you'll use `hanna /path/to/folders/*.rb` to generate your tests.

Anytime you get stuck, `rm -rf doc` and regenerate your docs.,