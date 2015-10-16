---
published: true
title: Value Object Tenants
layout: post
tags: [ruby, patterns]
categories: [ruby]
summary: How to use and work with a core OO paradigm.
---
Tenants of value objects:

1. A value object never changes the state of your application

2. A value object presents data and allows you to pose questions to the data

Some only provide the data, and convenient lookups

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
end
{% endhighlight %}

Others allow you to query data in a more advanced fashion.

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
      if client_id == ACTIVE[:beta] ||
         client_id == ACTIVE[:alpha] ||
         client_id == ACTIVE[:production_1]
      end
    end
  end
end

module Utilities
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
