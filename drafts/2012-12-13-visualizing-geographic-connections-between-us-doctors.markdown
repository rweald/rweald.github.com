---
layout: post
title: "Visualizing Geographic Connections Between US Doctors"
date: 2012-12-13 08:05
comments: true
categories: data R visualizations
---

I recently acquired access to the [DocGraph](http://strata.oreilly.com/2012/11/docgraph-open-social-doctor-data.html) data set on
[MedStartr](http://www.medstartr.com/projects/93-phase-ii-next-level-doctor-social-graph). 
This data set represent contains a social network of U.S. doctors, where each connection in the social network represents 
a physician referring a patient to another physician. 

Given this data set I thought it would be interesting to investigate the geographic connections between doctors. 
I took a sample of 1 million connections from the 
[DocGraph](http://strata.oreilly.com/2012/11/docgraph-open-social-doctor-data.html) and combined it with the [National Provider Identifier](http://en.wikipedia.org/wiki/National_Provider_Identifier) (NPI) database.
By combining these two data sets I was able to get the zip code of each physicians practice. I then took the zip codes and transcribed them into latitude-longitude coordinates using a 
a [publicly available database](http://federalgovernmentzipcodes.us/).

Once I had the coordinates for the doctors in the social network I decided to visualize the connections. 
My visualization was heavily inspired by the great work of
work of [Paul Butler at Facebook](http://www.facebook.com/notes/facebook-engineering/visualizing-friendships/469716398919).

Using a similar method to the one documented in [Nathan Yau's tutorial](http://flowingdata.com/2011/05/11/how-to-map-connections-with-great-circles/) I graphed the
connections between physicians using [great circles](http://en.wikipedia.org/wiki/Great_circle). 
Below is the resulting visualization which shows some interesting areas of high and low density.
All of the code used to generate this visualization is open source and can be found on [Github](https://github.com/rweald/docgraph-data-analysis/tree/master/visualize-geographic-connections)

![](https://s3.amazonaws.com/rweald-docgraph-analysis/map-of-connections-with-text-thumbnail.png)

You can download the full sized graphic [here](https://s3.amazonaws.com/rweald-docgraph-analysis/map-of-connections-with-text-fullsize.png)


This visualization is only the beginning. More work can be done to analyze the this social network with the added context of geographic location.
I would love to collaborate on some research related to analyzing the [DocGraph](http://strata.oreilly.com/2012/11/docgraph-open-social-doctor-data.html)
data set. If you are interested in collaborating research related to DocGraph please email me ryan \[at\] weald.com or message me on twitter [@rweald](http://twitter.com/rweald)

