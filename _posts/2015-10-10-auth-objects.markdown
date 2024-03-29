---
published: true
title: Authorization Objects
layout: post
tags: [ruby]
categories: [ruby]
summary: Don't allow permissions to mix with app state.
---

### Scenario

We run a youtube production company and we make videos for paying members.
Paying members can likewise access paid for premium content, and guests can access free content.
Pretty straight forward.

### Occurrence

We decide, one day, to open source all of our content. All videos, text posts, tutorials, etc
are now available to *all* users.

What's an optimal way to be able to ship this new business requirement?

Well, an "Authorization Object" (aka Query Object) isn't the worst way to go.

Here's an example of how we might use one here.

Example controller

{% highlight ruby %}
class SessionsController < Devise::SessionsController

  def new
    super
    redirect_to super_secret_admin_url if @authorizer.admin?
    redirect_to content_url if @authorizer.has_access_to_content?
    redirect_to guest_url if @authorizer.has_no_permissions?
  end

  private
  def authorizer
    @_authorizer ||= Authorizer.new(MaybeUser.new(current_user))
  end
end
{% endhighlight %}

Pretty basic login override controller here. The one cool thing we are doing is with regard to that
`Authorizer` class you see. First, we are memoizing it, and then we are initiailizing an instance of `Authorizer`
passing in the `current_user`. But, because the `current_user` could be null, we pass in a monad that will
return a non-null result and know how to handle a null user. Some people would have passed in a "Null Object",
but I'm more of a fan of the `MaybeUser` haskell-esque naming paradigm.

Here's how the `Authorizer` class might look.

{% highlight ruby %}
class Authorizer
  def initialize user
    @user = user
  end

  def admin?
    @user.admin
  end

  def has_access_to_content?
    if @user.admin || Receipt.find_by(cardholder_name: @user.name)
      true
    else
      false
    end
  end

  # This is just so we don't have to keep writing methods to check perms and this
  # makes it so we can use expressive methods like @authorizer.not_accessible
  # or @authorizer.has_no_permissions? as you see above, and it'll always return false.
  def method_missing
    false
  end
end
{% endhighlight %}

Notice how straight forward that was. We are doing no fancy tricks, but we still are wrapping
user query methods in what is essentially a "query object". This will become very obviously helpful in a minute.

*Uh-oh the boss wants to open source everything*

We want to open it all up. All users can access all content.

This is what's nice about having the authorizer already set up throughout our code base. We can
just inherit from it, return true on all methods and then swap it in. Alternatively, we could just
modify the auth object itself to return true and then we wouldn't have to swap it out.

{% highlight ruby %}
class VoidAuthorizer < Authorizer
  def has_access_to_content?
    true
  end

  def method_missing
    true
  end
end
{% endhighlight %}

Then, we change API where we implemented it, and that's basically it.

{% highlight ruby %}
def authorizer
  @_authorizer ||= VoidAuthorizer.new
end
{% endhighlight %}

Such is the beauty of seperating your logic from your state.
