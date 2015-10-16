---
published: true
title: Coupling & Cohesions
layout: post
tags: [ruby,patterns]
categories: [ruby]
summary: We run a youtube production company and we make videos for paying members. 

---

Scenario:

We run a youtube production company and we make videos for paying members.
Paying members can likewise access paid for premium content, and guests can access free content.
Pretty straight forward.

Next Scenario:
We decide, one day, to open source all of our content. All videos, text posts, tutorials, etc
are now available to *all* users.

What's the most optimal way to be able to ship such a feature, with all tests passing.

Well, an AuthorizationObject isn't the worst way to go.
Here's an example of how we might use one here.

Example controller

{% highlight ruby %}
class SessionsController < Devise::SessionsController
  before_filter :set_auth_object

  # Login example.
  # Do normal login, then goto route based on access level.
  def new
    super
    redirect_to super_secret_admin_url if @user_authorizer.admin?
    redirect_to content_url if @user_authorizer.has_access_to_content?
    redirect_to guest_url if @user_authorizer.has_no_permissions?
  end

  private
  # Create our auth object to ask it questions about the users permissions.
  def set_auth_object
    if user_signed_in?
      @user_authorizer = Authorizer.new(current_user)
    else
      @user_authorizer = Authorizer.new(:guest)
    end
  end
end
{% endhighlight %}

Here's how an example implementation of that auth object might look.

{% highlight ruby %}
class Authorizer
  def initialize user
    @user = user
  end

  def admin?
    @user.admin
  end
{% endhighlight %}

Here we are choosing rudimentary booleans just as an example.

{% highlight ruby %}
  def has_access_to_content?
    # Examples ideas on random ways a user could have access
    if @user.admin || @user.has_purchased
      true
    elsif Receipt.find_by(cardholder_name: @user.name)
      true
    else
      false
    end
  end
end
{% endhighlight %}

But.. now we want to open it all up. All users can access all content.
Well, an easy way to do that now would be to just subclass the main auth object
implement all the methods, return true, and profit.

{% highlight ruby %}
class VoidAuthorizer < Authorizer
  def has_access_to_content?
    true
  end
end
{% endhighlight %}

Then, we change API where we implemented it, and that's basically it.

{% highlight ruby %}
VoidAuthorizer.new
{% endhighlight %}

Such is the beauty of auth objects.