---
layout: post
title: "Spark Meetup: Monoids, Store, and Dependency Injection - Abstractions for Spark Streaming Jobs"
date: 2014-01-20 18:41
comments: true
categories: talk data Scala distributed-systems
---

Below is the presentation I gave at the Spark User Meetup on 01/16/2014


### Monoids, Store, and Dependency Injection - Abstractions for Spark Streaming Jobs

#### Abstract: 
One of the most difficult aspects of deploying spark streaming as part of your technology stack is maintaining all the code associated 
with stream processing jobs. In this talk I will discuss the tools and techniques that Sharethrough has found most useful for maintaining a large number of spark streaming jobs. 
We will look in detail at the way Monoids and Twitter's Algebrid library can be used to create generic aggregations.
 As well as the way we can create generic interfaces for writing the results of streaming jobs to multiple data stores.
 Finally we will look at the way dependency injection can be used to tie all the pieces together, enabling raping development of new streaming jobs.

<iframe width="560" height="315" src="http://www.youtube.com/embed/C7gWtxelYNM" frameborder="0" allowfullscreen></iframe>
<script async class="speakerdeck-embed" data-id="916d7bc061cf0131881c3e1e04cfd46e" data-ratio="1.2994923857868" src="//speakerdeck.com/assets/embed.js"></script>
