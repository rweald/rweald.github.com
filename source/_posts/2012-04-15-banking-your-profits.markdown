---
layout: post
title: Banking Your Profits, How to upgrade to Rails 3
summary: Technique you can use to improve your codebase while upgrading to a major version of rails
---
Let me start off by saying this is not a post touting all the great new features available in the latest version of Rails. I am not going to try and convince you that there is no way you can be productive staying on your current version of Rails. Instead this is a post about the way you can improve the overall quality of your codebase and reduce technical debt even if you never fully complete the upgrade. I am going to outline the process that we used at [Sharethrough](http://sharethrough.github.com) to improve the quality of our codebase while upgrading from Rails 2 to Rails 3.

The driving principle behind this post is "Banking your profits". In
software development that means making small focused commits on your
master branch and using *continuous integration*\[[1](#ci)\] to get those small changes integrated with the rest of your production code. By banking these profits along the way you gaining value even if you never succeed with the larger effort.

So how can you possibly make small focused commits when you are working on an undertaking as monumental as a Rails 3 upgrade?
The key to our success was small short lived Branches. The rules that governed these branches are as follows:

1) No branch may live longer than 24 hours  

2) You can not make any unnecessary changes that could not be backported.  

Following these rules you are able to shift your mindset. Rather than an
all or nothing sprint we instead methodically identified technical debt
that was hindering the upgrade but not directly a result of Rails API
incompatibilities. It was really quite amazing how much of the upgrade
pain was actually the result of tight coupling and
*SOLID*\[[2](#solid)\] design principle violations rather than Rails 3 incompatibilities.

Whenever we encountered a piece of debt that was hindering our upgrade we would switch back to the master branch and fix the code. Following this method the all or nothing part of the upgrade only took 2 days! The best part was even if we had never succeeded on the final portion of the upgrade we would have drastically improved the quality of the code allowing the team to move faster.

If you follow the technique outlined here you will improve the quality of your codebase regardless of whether the upgrade is successful. 

P.S. 

Want to work with me tackling hard problems across the stack using TDD and pair programming?
[Sharethrough is hiring talented engineers](http://www.sharethrough.com/engineering/)

<a name="ci"></a> \[1\] [http://en.wikipedia.org/wiki/Continuous_integration](http://en.wikipedia.org/wiki/Continuous_integration)

<a name="solid"></a> \[2\] [http://en.wikipedia.org/wiki/SOLID_\(object-oriented_design\)](http://en.wikipedia.org/wiki/SOLID_\(object-oriented_design\))
