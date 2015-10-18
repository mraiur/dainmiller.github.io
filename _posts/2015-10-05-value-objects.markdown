---
published: true
title: Value Object Tenants
layout: post
tags: [ruby, patterns]
categories: [ruby]
summary: How to use and work with a core OO paradigm.
---

Value objects are super interesting. To me, a value object is something we can use
to either wrap up data or ask questions of data.

The tenants might be: a value object never changes the state of your application, and 
a value object presents data and allows you to ask questions of the data.

Here's an example of what a few might look like.

{% highlight ruby %}
module Utilities
  class Sort
    ASC = "ASC" 
    DESC = "DESC"
    TYPES = {
      ascending: ASC,
      descending: DESC
    }
  end
  class HttpStatusCodes
    # Anytime we use a new code, add it to hash.
    CODES = {
      ok: 200,
      created: 201,
      temporary_redirect: 307,
      bad_request: 400,
      unauthorized: 401,
      request_timeout: 408
    }
  end
end
{% endhighlight %}

These are super simple. It just provided us a convenient way to lookup different
sorting paradigms. And you might think this is overkill, but when you have multiple developers
typing raw strings into complex methods you will very much wish you had an abstraction that allowed
them to *not* make a typo. Also, you could test these technically.

Here's an example of one that follows tenant #2. 

{% highlight ruby %}
module Utilities
  class ClientIds
    ACTIVE = {
      alpha: "id1",
      beta: "id2",
      production_1: "id3"
    }
    INACTIVE = {}

    def self.active? client_id
      ACTIVE.values.any? { |id| client_id == id }
    end
  end
end

{% endhighlight %}

As you can see in the above example here we aren't only providing the data in a nice wrapped up 
abstraction, we are also allowing objects outside of this class to ask questions of this data. 
This is where we get the real power of value objects. As system complexity grows, this can reduce a lot
of cognitive overhead. You shouldn't ever have to think "Oh shoot, what is this string representing".
