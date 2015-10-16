---
published: true
title: Value Objects in Ruby
layout: post
---
Tenants of value objects:
1. A value object never changes the state of your application
2. A value object presents data and allows you to pose questions to the data

Some only provide the data, and convenient lookups

```
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
```

```
module Utilities
  class ClientIds
    ACTIVE = {
      alpha: "f3de73ad8dbf6842814c5839490ae3ff",
      beta: "711d9c80d73d4be3d3ed58af6135555e",
      production_1: "f35b4c68254c7ea329c7b2558353b31e"
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
end```