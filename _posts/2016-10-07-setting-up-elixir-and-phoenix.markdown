---
published: true
title: Setting Up Elixir & Phoenix
layout: post
tags: [elixir, phoenix]
categories: [elixir]
summary: Up and running with the hotness.
---

Elixir and Phoenix. You know them, you want to learn them more.

Let me help.

## Install Process
<br />
Let's install Elixir, right off the bat.

```elixir
brew install elixir
```

Elixir's package manager `mix` is part of the Elixir standard library. How
amazing is that?

Now let's walk through the *painless* process to launch a new
[phoenix](http://www.phoenixframework.org/docs/installation) application.

1. Let's first install the additional `hex` package manager via `mix`. As you
   know by now in 2016, package managers installing package managers installing
   package managers has become common place - however meta it may be.

```elixir
mix local.hex
```

2. Next we have to install the "Phoenix" zip file (latest version) and let it
   build itself so that you can launch phoenix apps through `mix`.

```elixir
mix archive.install
https://github.com/phoenixframework/archives/raw/master/phoenix_new.ez
```

3. We can test our Elixir and Phoenix install process by running the following
   command to build a blank app.

```elixir
mix phoenix.new web --no-brunch --no-ecto
```

Success! 2 steps. Can you believe it?

## Elixir & Phoenix Core Packages 
<br />
Here are the things you need to know:

[ecto](http://www.phoenixframework.org/docs/ecto-models) is the ORM for Elixir, similar to
[ActiveRecord](http://guides.rubyonrails.org/active_record_basics.html) for Rails.

[mix](http://elixir-lang.org/getting-started/mix-otp/introduction-to-mix.html) is the package manager for Elixir. Similar to `gem install` via
[Rubygems](https://rubygems.org/).

[exunit](http://elixir-lang.org/docs/stable/ex_unit/ExUnit.html) is the commonly used testing framework for Elixir. Similar to `rspec` in Rails.

[postgres](https://www.postgresql.org/) support comes built in from the beginning when you boot a Phoenix app.
