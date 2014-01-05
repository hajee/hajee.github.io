---
layout: post
title: "On your way to easier deployments?"
date: 2013-10-17 16:15:13 +0100
comments: true
categories: ['devops','method']
keywords: devops, continuous deployment, continuous integration
description: How to get the discussions started about faster and more deployments
---
In [my last blog post]({% post_url 2013-10-02-visualize-your-continuous-deployment-maturity %}), I described the main area's of interest to work on to get faster and easier deployments. For every area,  the level of maturity may be different. In this blog post,  I will dive deeper in the levels of maturity and what they mean.

<!-- more -->

Like I told in the previous blog posts, this information is based on the book ["Continuous Delivery"](http://www.amazon.com/gp/product/0321601912?ie=UTF8&tag=martinfowlerc-20&linkCode=as2&camp=1789&creative=9325&creativeASIN=0321601912) by [Jez Humble](http://jezhumble.net/) and [David Farley](http://www.davefarley.net/)

#The Five maturity levels

In the model, they describe the following five levels.

0. Regressive
1. Repeatable
2. Consistent
3. Quantitatively managed
4. Optimizing

{% img /images/maturity-levels.png The levels of maturity %}


### Regressive

There is no process for releasing and delivering software. A new deployment becomes an intensive event with a lot of opportunity to fail. A successful deployment is a victory. Although the number in the list says 1. In their book, Jez and David call the level -1. Minus because deployment is actually in the toddler stage.

###Repeatable
When you are at this level of maturity, some stuff is being take care of. Changes management processes are in lace. There are clear guidelines of what to do and when to do it. Most of the times the organisations have a OTAP strategy, but most of the testing is done by humans. Only a small part of the tests, if any, is automated. Not a lot has been done to automate deployment. Most of the work is done by typing commands on a terminal based on a script in a paper document. In my view,  this is the minimum level at which you can rightfully claim you are doing [ITIL](http://en.wikipedia.org/wiki/Information_Technology_Infrastructure_Library#ITIL_V3). As you can see this is still much lower than the levels proposed in [the book](http://www.amazon.com/gp/product/0321601912?ie=UTF8&tag=martinfowlerc-20&linkCode=as2&camp=1789&creative=9325&creativeASIN=0321601912)

###Consistent
At this level of maturity,  you have a broad set of automated tests. The tests are  at a sufficient level to detected critical errors early end often. The deployment is getting more and more automated. Deploying a new version to an integrated testing environment becomes easy.

###quantitatively managed
The testing and deployment are fully automated, and there is a pipeline in place to do the testing and deployments in OTAP environments. Bad versions are caught in the deployment pipeline before they reach production. Because deployments are easy and the quality of releases increase, teams start to do more and smaller deployments. The statistics of builds and deployments are tracked, and acted upon.

###optimizing
At the final level, not only all processes and tools are in place, but the whole organisation around building, testing and deploying software is constantly improving. Teams regularly discuss the problems and fix them. Every deployment, whether it is in production or any test environment is a vehicle for improvement.

