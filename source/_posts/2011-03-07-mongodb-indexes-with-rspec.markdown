---
layout: post
tite: Testing MongoDB Spatial Queries With Rspec
summary: A brief overview of one common pitfall regarding testing geo-spatial queries
---

I recently had need to test some geospatial queries in a rails
application.
At first this seems like nothing out of the ordinary but there are 
a couple of minor details that if forgotten can result in failing tests

The main difference between geo queries and your average run of the mill
query is the need for and index. 
Normally when a simple unit test suite is run you don't worry about
building indexes as you wont be querying large amounts of data to speed 
is not an issue. Besides if you are reading this you are using Rspec 
which means you are not too concerned with your test speed.

However, if you want to test geo queries in MongoDB you will have to 
ensure that your index is built or the query can not be executed.
This is because geospatial queries can only be run against a special 2D index 
and not against the underlying data. 

Now the obvious solution would be to place some code in your
spec_helper file that will create the indexes. 
I felt like this was a bit to heavy handed since I only wanted 
to test the geospatial queries in 1 describe block. 

So to fix the problem I choose to add a call to Mongoid::Indexes create_indexes
method within my before block. 

{% codeblock lang:ruby %}
describe ".guides_nearby" do
  before(:each) do
    @guide = Factory(:guide)
    Guide.create_indexes
    @result = Guide.guides_nearby("San Diego,United States")
  end
  it {@result.first.should == @guide}
end
{% endcodeblock %}
