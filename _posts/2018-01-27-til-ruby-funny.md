---
layout: default
title:  "Ruby funny!"
date:   2018-01-27 15:30:46 +0700
categories: til
---

Some magic code in ruby and rails seem to be implemented easily

## helper_method
```ruby
# Declare controller method as helper
class TodoController
  helper_method :login?

  def login?
  end
end

# Using in view (*.html.slim)
- if login?
 = render 'Logout'

```

## Call helper method in controller without conflict controller method (>= rails 5)
+ <https://blog.bigbinary.com/2016/06/26/rails-add-helpers-method-to-ease-usage-of-helper-modules-in-controllers.html>

```ruby
# helpers.helper_method
class TodoController
  def show
    message = "#{helpers.helper_method}"
  end
end
```

## Ruby yield, block
+ <https://mixandgo.com/blog/mastering-ruby-blocks-in-less-than-5-minutes>

```ruby
class Test
  def show_name # Or: def show_name(&block)
    p 'top'
    yield # Or: block.call
    p 'bottom'
  end
end

a = Test.new
a.show_name do
  p 'middle'
end
```

## Create default value for object with yield
+ <https://robots.thoughtbot.com/mygem-configure-block>

```ruby
module Test
  class << self
    attr_accessor :configuration
  end

  def self.configure
    self.configuration ||= Configuration.new
    yield(configuration)
  end

  class Configuration
    attr_accessor :name
  end
end

Test.configure do |config|
  config.name = 'quyen'
end

p Test.configuration
#<Test::Configuration:0x007f9c8507acc8 @name="quyen">
```

## Example using macro in Rails
+ <https://pragmaticstudio.com/tutorials/ruby-macros>

```ruby
class ActiveRecord
  def self.has_many(source)
    # def comments
    # end
    define_method(source) do
      p '#{source} method created'
    end
  end
end

class Post < ActiveRecord
  has_many :comments
  has_many :reviews
end

post = Post.new
post.comments
```