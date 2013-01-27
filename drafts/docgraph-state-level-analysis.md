---
layout: post
title: "Analyzing Inter-State Patient Referrals"
date: 2013-01-27 11:48
comments: true
categories: data R visualizations docgraph
---

I previously built a [visualization of the U.S. medical graph](http://isurfsoftware.com/blog/2012/12/13/visualizing-geographic-connections-between-us-doctors/) using the 
[DocGraph](http://strata.oreilly.com/2012/11/docgraph-open-social-doctor-data.html) dataset.
The visualization prompted me to ask the question, does the state where you live affect the likelihood you will be referred to a doctor in another state?

Using the full [DocGraph](http://strata.oreilly.com/2012/11/docgraph-open-social-doctor-data.html) dataset I was able to answer this question; in short North Carolina had the highest percentage of patients referred out of state with ~ 28% of referrals going out of state. Michigan and California had the lowest percent with only ~10% of referrals going out of state. 

In the remainder of this post I shall describe the process I used to obtain these result and provide a more detailed look at the impact state has on probability of inter-state referrals.

The first step in the analysis was joining the DocGraph referral graph with the 
[National Provider Identifier database](http://www.cms.gov/Regulations-and-Guidance/HIPAA-Administrative-Simplification/NationalProvIdentStand/index.html). 
By joining DocGraph with the NPI database I was able to determine the state of the referring physician as well as the state of the physician the patient was being referred to. After augmenting the DocGraph with this additional information it was simply a matter of aggregating referrals grouped by state. Once aggregated I had a state to state adjacency matrix which could be further aggregated to generate the graphs shows below.

For details on reproducing this analysis and all the code used [visit Github](INSERT_LINK)

Below is a [choropleth map](http://en.wikipedia.org/wiki/Choropleth_map) representing the percent of patients that were referred outside of the state. As you can see North Carolina, Pennsylvania have the highest percent out of state referrals. There is also an area of increased out of state referrals in the [mountain region](http://en.wikipedia.org/wiki/File:Census_Regions_and_Division_of_the_United_States.svg).

<div style="border: 1px solid black;">
  <a href="http://bit.ly/Wvyfes" >
    <img src="https://s3.amazonaws.com/rweald-docgraph-analysis/percent-leaving-state-choropleth-dev.png" alt="percent-out-of-state-referrals" height=450 width=800 />
  </a>
</div>

A complement to the above image is shown below; The color represents the percent of patients that are referred within the same state. As you would expect the larger states such as California, Texas, and New York have the highest percentage of patients referred within the same state.

<div style="border: 1px solid black;">
  <a href="http://bit.ly/X4RRH9">
    <img src="https://s3.amazonaws.com/rweald-docgraph-analysis/percent-in-state-choropleth-dev.png" alt="percent-in-state-referrals" height=450 width=800 />
  </a>
</div>

For those readers who want more detail on the statistical distributions of out of state referrals below you'll find [kernel density estimate](http://en.wikipedia.org/wiki/Kernel_density_estimation) plots.

<div style="border: 1px solid black;">
  <a href="http://bit.ly/WhQSVV">
    <center>
      <img src="https://s3.amazonaws.com/rweald-docgraph-analysis/general-statistical-plots.png" alt="percent-in-state-referrals" height=360 width=640 />
    </center>
  </a>
</div>


After analyzing the number of out of state referrals I got curious where all these out of state referrals were going. As a first step towards understanding out of state referrals I assembled a [heat map](http://en.wikipedia.org/wiki/Heat_map). This heat map provides some details on which states patients are being referred to. Each square in the heat map represents an entry in the state to state adjacency matrix contained in the DocGraph network.

<div style="border: 1px solid black;">
  <a href="http://bit.ly/W9mpdx">
    <img src="https://s3.amazonaws.com/rweald-docgraph-analysis/inter-state-referrals-heatmap.png" alt="inter-state-referral-heatmap" height=450 width=800 />
  </a>
</div>

This analysis brings us one step closer to unlocking the potential of the [DocGraph](http://strata.oreilly.com/2012/11/docgraph-open-social-doctor-data.html) data in helping us understand the U.S. health graph. 

There are a couple of important limitations of the data to remember when interpreting this analysis. The DocGraph data set only includes data from 2011; we can assume that physician behavior is much the same today as it was in 2011, however without a sample from some other time period we can not be sure. Secondly, DocGraph only represents Medicare referrals which may not be representative of the entire healthcare system. Unfortunately a more comprehensive dataset including private referrals is not available to me at this time. Therefore, the DocGraph dataset is the best referral sample I could get as a private citizen.

I hope you have enjoyed my analysis. 
I am always open to feedback and would love to collaborate on some research related to analyzing the [DocGraph](http://strata.oreilly.com/2012/11/docgraph-open-social-doctor-data.html)
data set. 
If you are interested in collaborating on research related to [DocGraph](http://strata.oreilly.com/2012/11/docgraph-open-social-doctor-data.html)
 please email me ryan \[at\] weald.com or message me on twitter [@rweald](http://twitter.com/rweald)

