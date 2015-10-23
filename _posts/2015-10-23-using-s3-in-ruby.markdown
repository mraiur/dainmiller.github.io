---
published: true
title: Using S3 in Ruby
layout: post
tags: [ruby, aws]
summary: A simple way to interface with AWS's S3.
---
I wrote an incredibly simple S3Importer class in Ruby today using the AWS-SDK v2.0 gem. It seemed useful, so I thought I'd share. 

What I like about it:

1. Setting buckets as constants, alleviate typos from others developers using this class

What I don't like:

1. The buckets should really be in a seperate class, so that they can be mixed into other S3Verb classes, for instance maybe we have an S3Downloader class, we should be able to mixin the buckets available to us in a value object.

{% highlight ruby %}
class S3Importer
  BUCKETS = {
    bucket_name: 'bucket_name'
  }
  
  def initialize
    @s3 = AWS::S3.new.buckets[BUCKETS[:bucket_name]]
  end

end

  def import! 
    @s3.objects.each { |object| do_something_with_object(object) }
  end
end
{% endhighlight %}
