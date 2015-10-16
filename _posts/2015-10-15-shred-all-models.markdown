---
published: false
title: Shred All Models
layout: post
---
{% highlight ruby %}

  module Util
    def self.shred_everything!
      return unless Rails.env.development? || Rails.env.test?

      models = Dir.glob("#{ Rails.root }/app/models/*.rb").collect do |file|
        base = File.basename(file)
        base.gsub!('.rb','')

        base.camelize.constantize rescue nil
      end.compact

      models.select! {|m| m.respond_to?(:delete_all) }

      models.each(&:delete_all)
    end
  end

{% endhighlight %}
