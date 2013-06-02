---
layout: post
title: "Analyzing DocGraph - What Type of Doctor Will You See Next?"
date: 2013-06-02 09:29
comments: true
categories: data R docgraph
---

In my previous posts analyzing the [DocGraph](http://docgraph.org/?page_id=4) dataset I have looked at 
[the geographic connections between referrals](http://isurfsoftware.com/blog/2012/12/13/visualizing-geographic-connections-between-us-doctors/) and
[out of state referrals](http://isurfsoftware.com/blog/2013/01/27/analyzing-out-of-state-patient-referrals-using-docgraph/). In this post I decided to change
directions from geographic analysis and instead focus on the different types of providers involved in patient referrals. In particular I wanted to take a crack at answering the question:
"what type of doctor will you see next?"

As always the first step to answering this question was to enrich the [DocGraph](http://docgraph.org/?page_id=4) data with data from the NPI database. In particular we need the taxonomy code for each of the nodes in the [DocGraph](http://docgraph.org/?page_id=4) dataset.
After the we have added taxonomy code to all the nodes we then want to aggregate all referrals by taxonomy code to shrink the size of our dataset down into something that is more easily managed on a single machine.
In order to achieve this goal with short iteration time I used [Amazon EMR](http://bit.ly/10RKWmf) and [Apache Hive](http://hive.apache.org/). The distributed nature of [Hadoop](http://hadoop.apache.org/) and [Hive](http://hive.apache.org/) enabled me to join the large
NPI database with the even larger [DocGraph](http://docgraph.org/?page_id=4) dataset and perform the necessary aggregation all in under 20 minutes with a cost of only $1.04. You can find the Hive script I used to perform the join and aggregation on [Github](http://bit.ly/16Br1Qo).

Once the Docgraph dataset had been aggregated by taxonomy code it was a simple matter of converting the taxonomy code to the human readable provider type. This was achieved using the [Health Care Provider Taxonomy dataset](http://www.nucc.org/index.php?option=com_content&view=article&id=14&Itemid=125) 
and some R code that you can find on [Github](http://bit.ly/11O4FrY). A little bit more aggregation to account for the multiple levels of taxonomy codes, including specialization, and the data needed to answer our question was ready. I also removed any referrals where both nodes were of the same provider
type as these are most likely noise in the dataset caused by the billing method through which the [DocGraph](http://docgraph.org/?page_id=4) data was collected.

Below is a table showing the top 20 referrals between provider types. Not surprisingly we can see that the vast majority of patients are being referred for to Radiology 
for various types of test such as X-rays, CT scans, and MRIs. They are then referred back to an _Internal Medicine_ doctor which I hypothesize is the physician acting as primary care.
Another interesting, but not all that surprising, relationship is the number of referrals between _Emergency Medicine_ and _Internal Medicine_. Here I hypothesize that patients are being
seen for some emergency medical condition and then receive follow-up care from their primary care provider.

Perhaps the most interesting observation from this top 20 list is the number of times _Internal Medicine - Cardiovascular Disease_ appears. I always knew that America had a problem with heart disease but I was still a bit surprised at the volume of this type of referral. I would love to hear if anyone else has a hypothesis for why there are so many referrals 
related to _Internal Medicine - Cardiovascular Disease_.


<table border=0 class="table table-bordered table-striped">
  <tbody> 
    <tr class= firstline > 
      <th>type.x  </th>
      <th>type.y  </th>
      <th>num_patients</th> 
    </tr> 
    <tr> 
      <td class=cellinside>Radiology - Diagnostic Radiology
      </td>
      <td class=cellinside>Internal Medicine - General
      </td>
      <td class=cellinside>115,602,860
    </td></tr>

    <tr> 
      <td class=cellinside>Internal Medicine - General
      </td>
      <td class=cellinside>Radiology - Diagnostic Radiology
      </td>
      <td class=cellinside> 91,632,055
    </td></tr>

    <tr> 
      <td class=cellinside>Internal Medicine - Cardiovascular Disease
      </td>
      <td class=cellinside>Internal Medicine - General
      </td>
      <td class=cellinside> 54,260,749
    </td></tr>

    <tr> 
      <td class=cellinside>Radiology - Diagnostic Radiology
      </td>
      <td class=cellinside>Internal Medicine - Cardiovascular Disease
      </td>
      <td class=cellinside> 49,406,691
    </td></tr>

    <tr> 
      <td class=cellinside>Internal Medicine - Cardiovascular Disease
      </td>
      <td class=cellinside>Radiology - Diagnostic Radiology
      </td>
      <td class=cellinside> 47,820,945
    </td></tr>

    <tr> 
      <td class=cellinside>Internal Medicine - General
      </td>
      <td class=cellinside>Internal Medicine - Cardiovascular Disease
      </td>
      <td class=cellinside> 47,351,852
    </td></tr>

    <tr> 
      <td class=cellinside>Radiology - Diagnostic Radiology
      </td>
      <td class=cellinside>Family Medicine - General
      </td>
      <td class=cellinside> 45,078,839
    </td></tr>

    <tr> 
      <td class=cellinside>Family Medicine - General
      </td>
      <td class=cellinside>Radiology - Diagnostic Radiology
      </td>
      <td class=cellinside> 40,181,846
    </td></tr>

    <tr> 
      <td class=cellinside>Emergency Medicine - General
      </td>
      <td class=cellinside>Radiology - Diagnostic Radiology
      </td>
      <td class=cellinside> 33,797,598
    </td></tr>

    <tr> 
      <td class=cellinside>Emergency Medicine - General
      </td>
      <td class=cellinside>Internal Medicine - General
      </td>
      <td class=cellinside> 32,236,140
    </td></tr>

    <tr> 
      <td class=cellinside>Radiology - Diagnostic Radiology
      </td>
      <td class=cellinside>Specialist - General
      </td>
      <td class=cellinside> 27,710,610
    </td></tr>

    <tr> 
      <td class=cellinside>Specialist - General
      </td>
      <td class=cellinside>Internal Medicine - General
      </td>
      <td class=cellinside> 26,478,301
    </td></tr>

    <tr> 
      <td class=cellinside>Internal Medicine - General
      </td>
      <td class=cellinside>Specialist - General
      </td>
      <td class=cellinside> 24,876,128
    </td></tr>

    <tr> 
      <td class=cellinside>Specialist - General
      </td>
      <td class=cellinside>Radiology - Diagnostic Radiology
      </td>
      <td class=cellinside> 23,929,823
    </td></tr>

    <tr> 
      <td class=cellinside>Radiology - Diagnostic Radiology
      </td>
      <td class=cellinside>Emergency Medicine - General
      </td>
      <td class=cellinside> 23,424,750
    </td></tr>

    <tr> 
      <td class=cellinside>Internal Medicine - General
      </td>
      <td class=cellinside>Family Medicine - General
      </td>
      <td class=cellinside> 22,561,522
    </td></tr>

    <tr> 
      <td class=cellinside>Radiology - Diagnostic Radiology
      </td>
      <td class=cellinside>Internal Medicine - Nephrology
      </td>
      <td class=cellinside> 22,479,825
    </td></tr>

    <tr> 
      <td class=cellinside>Radiology - Diagnostic Radiology
      </td>
      <td class=cellinside>Internal Medicine - Pulmonary Disease
      </td>
      <td class=cellinside> 21,796,186
    </td></tr>

    <tr> 
      <td class=cellinside>Family Medicine - General
      </td>
      <td class=cellinside>Internal Medicine - General
      </td>
      <td class=cellinside> 20,872,086
    </td></tr>

    <tr> 
      <td class=cellinside>Internal Medicine - Cardiovascular Disease
      </td>
      <td class=cellinside>Family Medicine - General
      </td>
      <td class=cellinside> 19,047,613
    </td></tr>

  </tbody>
</table>

If you would like to see more than just the top 20 referrals by provider type you can download the complete list [here](http://bit.ly/19zzTER)

Finally, I can't resist a sexy visualization that helps to convey the elegance of the [DocGraph](http://docgraph.org/?page_id=4) dataset. Below you will find a visualization of the
referrals between provider types. The thickness of the edge reflects the number of patients that are referred between the two provider types. To create the visualization I used the open source [Gephi](http://gephi.org/) graph visualization platform.


<span style="font-size: 0.8em; font-style: italic;">
  click on the image below to see the full size version
</span>

<a href="http://rweald-docgraph-analysis.s3.amazonaws.com/referrals-by-provider-graph.png">
  <img src="http://rweald-docgraph-analysis.s3.amazonaws.com/referrals-by-provider-graph.png" width=800 height=800 alt="visualization of referrals by provider"/>
</a>

I hope you have enjoyed my analysis. 
I am always open to feedback and would love to collaborate on analysis related [DocGraph](http://strata.oreilly.com/2012/11/docgraph-open-social-doctor-data.html) or open health data in general.
If you are interested in collaborating please email me ryan \[at\] weald.com or message me on twitter [@rweald](http://twitter.com/rweald)
