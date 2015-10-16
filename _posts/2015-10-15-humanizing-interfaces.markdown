---
published: false
title: Humanizing Interfaces
layout: post
---
{% highlight ruby %}

class Manager 
  def initialize(*args)
    start_logger
  end
  
  def log_me
    # TODO: Add file
    @logger = Logger.new 'file'
  end
end
class QueueManager < Manager
  def initialize, options = {}
    @queues = []
    super
  end
  
  def start_queue amount
    1..amount.each { |count| @queues.push({"q#{count}": []}) }
  end
  
  def can_help? action, action_performed_on
    if @queue.any?
      @queue[0]['q1'].push(action_performed_on, action)
    end
  end
end


# Interface
manager = QueueManager.new
maanger.start_queue(1)
if manager.can_help?(:save, User.new(name: 'Dain'))
  redirect_to root_url
else
  raise QueueError, "No queue has been started."
end

{% endhighlight %}
