---
published: true
title: API Classes
layout: post
tags: [ruby, api]
summary: API connection and data transmutation examples.
---
Example code today, that's it. 

This was mostly taken from an amazing talk, and is not all my code. I will link the talk when I can find it.

{% highlight ruby %}
class Connection
  include HTTParty
  DEFAULT_VERSION = "1"
  DEFAULT_BASE_URI = "api_base_url_here"
  DEFAULT_QUERY = {}
	
  def initialize options = {}
    @api_version = options.fetch(:api_version, DEFAULT_API_VERSION)
    @query = options.fetch(:query, DEFAULT_QUERY)
  end
	
  def query params = {}
    @query.update(params)
  end	
end

# Implementation
connection = Connection.new(api_version: "1")
connection.query(key: "test")

class Client
  def initialize options = {}
    @connection = options.fetch(:connection)
    @routes = options.fetch(:routes)
  end
	
  def method_missing method
    route_map = routes.fetch(method)
    http_method = route_map.fetch(:method)
    relative_path = route_map.fetch(:path)	
	
    @connection.send(http_method, relative_path)
  end
end
	
routes = {
  route: {
    method: 'get',
    path: '/route'
  }
}

# Implementation
client = Client.new(connection: connnection, routes: routes)

class Representation < OpenStruct
  attr_reader :parent, :children
	
  def init rep = {}, parent = nil
    super rep
    @parent = parent
    @children = []
    bind parent
    represent children
  end
	
  def represent type, collection, parent=nil
    collection = Array(collection)
    collection.map do |item|
      definition_class = definition_class_for type
      definition_class.new item, parent
    end
  end
	
  def definition_class_for type
    definition_class = type.to_s.constantize
    Object.const_get definition_class
  rescue NameError
    Object.const_set definition_class, Representation
  end
end
{% endhighlight %}
