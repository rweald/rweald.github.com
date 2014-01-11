---
layout: post
title: "Spark Summit 2013 - Productionalizing Spark Streaming"
date: 2014-01-11 10:54
comments: true
categories: talk data Scala distributed-systems
---

Below is the presentation I gave at [Spark Summit 2013](http://spark-summit.org/summit-2013/)

### Productionalizing Spark Streaming

At Sharethrough we have deployed Spark to our production environment to support several user facing product features. While building these features we uncovered a consistent set of challenges across multiple streaming jobs. By addressing these challenges you can speed up development of future streaming jobs. In this talk we will discuss the 3 major challenges we encountered while developing production streaming jobs and how we overcame them.

First we will look at how to write jobs to ensure fault tolerance since streaming jobs need to run 24/7 even under failure conditions. Second we will look at the programming abstractions we created using functional programming and existing libraries. Finally we will look at the way we test all the pieces of a job –from manipulating data through writing to external databases– to give us confidence in our code before we deploy to production


<iframe width="560" height="315" src="http://www.youtube.com/embed/OhpjgaBVUtU" frameborder="0" allowfullscreen></iframe>
<script async class="speakerdeck-embed" data-id="a45f30f03dd70131600346451c48010b" data-ratio="1.2994923857868" src="//speakerdeck.com/assets/embed.js"></script>
