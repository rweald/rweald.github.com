---
layout: post
title: "Visualizing the Geographic Connections Between U.S. Doctors"
date: 2012-12-13 08:05
comments: true
categories: data R visualizations docgraph
---

I recently acquired access to the [DocGraph](http://strata.oreilly.com/2012/11/docgraph-open-social-doctor-data.html) data set on
[MedStartr](http://www.medstartr.com/projects/93-phase-ii-next-level-doctor-social-graph). 
This data set contains a social network of U.S. doctors, with each connection representing
a physician referring a patient to another physician. 
Given this new unique data I thought it would be interesting to investigate the geographic connections between doctors. What better way to start
analyzing the data than to make a sexy visualization.

To create the final visualization I had to combine multiple data sets to enrich the doctor social graph with geographic coordinates. 
I began by taking a sample of 1 million connections from
[DocGraph](http://strata.oreilly.com/2012/11/docgraph-open-social-doctor-data.html) and joining it with the 
[National Provider Identifier](http://en.wikipedia.org/wiki/National_Provider_Identifier) (NPI) database.
By joining these two data sets I was able to get the zip code of each physicians practice. The final step was converting the zip codes to 
latitude-longitude coordinates using
a [publicly available zip code database](http://federalgovernmentzipcodes.us/). Now that the data was in the correct format I began work on the visualization.

The visualization I choose was heavily inspired by the great
work of [Paul Butler at Facebook](http://www.facebook.com/notes/facebook-engineering/visualizing-friendships/469716398919).

Using a similar method to the one documented in [Nathan Yau's tutorial](http://flowingdata.com/2011/05/11/how-to-map-connections-with-great-circles/) I graphed the
connections between physicians using [great circles](http://en.wikipedia.org/wiki/Great_circle). In order to see the cluster density I layered the connections
using Euclidean distance, with the longest paths being drawn first.
All of the code used to generate this visualization is open source and can be found on [Github](https://github.com/rweald/docgraph-data-analysis/tree/master/visualize-geographic-connections)


Below is the resulting visualization. Note the areas of high and low density as you move from the east coast over to the west coast.
There are also some interesting connections from
Hawaii and Puerto Rico to the Continental United States.


<a href="https://s3.amazonaws.com/rweald-docgraph-analysis/map-of-connections-with-text-fullsize.png">
  <img src="https://s3.amazonaws.com/rweald-docgraph-analysis/map-of-connections-with-text-thumbnail.png" alt="Doctor to Doctor connections visualized" />
</a>

You can download the full sized graphic [here](https://s3.amazonaws.com/rweald-docgraph-analysis/map-of-connections-with-text-fullsize.png).
<span style="font-size: 0.8em; font-style: italic;">
  I recommend you right-click and "save link as" because the file is approximately 40MB.
</span>


This visualization is only the beginning. The added feature of geography opens the door to many interesting analyses.
I would love to collaborate on some research related to analyzing the [DocGraph](http://strata.oreilly.com/2012/11/docgraph-open-social-doctor-data.html)
data set. If you are interested in collaborating on research related to [DocGraph](http://strata.oreilly.com/2012/11/docgraph-open-social-doctor-data.html)
 please email me ryan \[at\] weald.com or message me on twitter [@rweald](http://twitter.com/rweald)

