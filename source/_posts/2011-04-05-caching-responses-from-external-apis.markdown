---
layout: post
title: Caching Responses From Remote APIs
summary: Discussion of the techniques used to limit the response time when making search requests to the mendeley api
---

  [Dokbot](http://secure.dokbot.com), the project that I am currently
working on, utilizes the mendeley API to add citations to posts. To 
achieve this the application allows users to click an add citation
button which brings up a modal view where the user can enter a search
term that will be sent off the the mendeley API. To provide the a
positive user experience the search form must be highly responsive. This
presented a problem because the [mendeley](http://mendeley.com) API
although resonably responsible was not quite snappy enought to provide
the UX we were looking for. 

  To remidy this problem we decided to route the search request through
our own application servers. Although at first glance this might appear
to be a bad idea as it would increase latency, it turns out it actual
decreased the average latency. The cause for this decrease in
latency; caching. It turns out that most users enter the same search
term almost every time they enter a citation. With this in mind we wrote
some code in our application that caches the responses from mendeley API
that way for any given search query we only have to make 1 request to
the mendeley API. All subsequent requests for the search term will be
returned from our application cache rather than a request to the API. 

  Caching was also a resonable solution for this particular problem
because the mendeley search results change very infrequently. 

You can see the code below that was used to cache the mendeley API
response using whatever cache [Rails](http://guides.rubyonrails.org/caching_with_rails.html) is configured to use. 

####The Code
{% codeblock lang:ruby %}
def self.search_mendeley(query=nil)
  raise "no query specified" unless query

  papers = Rails.cache.fetch(query) do |query|
    response = Mendeley::API::Documents.search(query)
    papers = response["documents"][0..5]
  end

  return papers
end
{% endcodeblock %}
