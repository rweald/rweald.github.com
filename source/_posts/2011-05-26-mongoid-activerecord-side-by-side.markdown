---
layout: post
title: Using Mongoid Alongside ActiveRecord
summary: A quick tutorial on how to configure your Rails 3 app to use Mongoid alongside ActiveRecord
---

MongoDB is a very popular document oriented database and more apps are
using it every day. However, we all know about the problems that mongo
has with data durability. So you might not want to use it as a complete
replacment for ActiveRecord and your favorite sql store. 
[Mongoid](http://mongoid.org) is an ActiveModel compliant ORM for
MongoDB. Below I will outline how you can use Mongoid alongside
ActiveRecord in your rails 3 app. 

1) Add mongoid to your gemfile
{% codeblock lang:ruby %}

  gem "mongoid", "~> 2.0"
  gem "bson_ext", "~> 1.3"

{% endcodeblock %}  

2) Run the mongoid generator in your projects root directory

{% codeblock lang:ruby %}
rails generate mongoid:config
{% endcodeblock %}  

This will generate a config/mongoid.yml file where you can configure
your connection to mongodb. 

3) Right now mongoid has overriden activerecord as the default orm so
any attempts to generate migrations or ActiveRecord models will fail. 
Therefore we must configure our default generators so we can still use
activerecord. 

To do that simple add the following line to your config/application.rb
file

{% codeblock lang:ruby %}
  config.generators do |g|
    g.orm :active_record
  end

{% endcodeblock %}  


