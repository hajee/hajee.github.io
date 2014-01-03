---
layout: post
title: "Want easier deployments?"
date: 2014-01-02 16:15:13 +0100
comments: true
categories: ['devops','method']
keywords: devops, continiuous deployment, continiuous integration
description: How to get the discussions started about faster and more deployments
---
Looking around the Internet, you see more and more companies starting to do multiple deployments per day. There are the [stories of Facebook deploying multiple times per day](https://www.facebook.com/notes/facebook-engineering/ship-early-and-ship-twice-as-often/10150985860363920). The stories of [The Guardian](http://blog.utest.com/continuous-deployment-and-testing-in-production/2012/12/) and many many more. If after reading these stories you feel like you want to move from your current one deployment per 3 month strategy to a more agile method, but have don't know where to start. This blog post might be of assistance.

<!-- more -->
In their 2010 seminal work ["Continuous Delivery"](http://www.amazon.com/gp/product/0321601912?ie=UTF8&tag=martinfowlerc-20&linkCode=as2&camp=1789&creative=9325&creativeASIN=0321601912) [Jez Humble](http://jezhumble.net/) and [David Farley](http://www.davefarley.net/) described a maturity model for continious delivery. The goal of this model was to asses the gap between where you are and where you want to be and help to define the steps you need to take to go there.

#What to measure?


#What's the scale
In the model they describe the following 5 levels.

###initial
There is no process for releasing and delivering software. A new deployment becomes a intensive event whith a lot of oportunaty to fail. A succesful deployment is a victory. 

###managed
When you are at this level, some stuff is beeing take care of. Changes management processes are in lace. There are clear guidelines of what to do and when to do it. Most of the times the organisations have a OTAP strategy, but most of the testing is done by humans.Only a small part of the tests, if any, is automated. Not a lot has been done to automate deployment. Most of the work is done by typing commands on a terminal based on a script in a paper document.

###defined
There are automated tests at a sufficent level to detected critical errrors early end often. The deployment is getting more and more automated. Deploying a new version to an integrated testing environment becomes easy.

###optimizing
The testting and deployment is fully automated and there is a pipeline in place to do the testing and deployments in OTAP environments. Bad versions are cought in the deployment pipeline before they reach production. Because deployments are easy and the quality of releases increase, teams start to do more and smaller deployments. 

###quantitatively managed
Systems are architected with continuous deployment in mind. All new requirements describe how the value of the feature will be measured in production.Metrics are gathered through techniques such as A/B testing to validate the value is actualy beeing delivered like expected. 

