---
layout: post
title: "Visualize your continuous deployment maturity"
date: 2013-10-02 16:15:13 +0100
comments: true
categories: ['devops', 'visualize']
keywords: devops, visualize, maturity level, continiuous deployment, continiuous integration
description: Visualize the levels of maturity at the six interest area's for continuous deployment
---
Looking around the Internet, you see more and more companies starting to do multiple deployments per day. There are the [stories of Facebook deploying multiple times per day](https://www.facebook.com/notes/facebook-engineering/ship-early-and-ship-twice-as-often/10150985860363920). The stories of [The Guardian](http://blog.utest.com/continuous-deployment-and-testing-in-production/2012/12/) and many more. If you want to go down that path, it really helps having a way of visualizing where you are, and where you want to go to. This helps the discussion with the stakeholders and gets things going. In this blog post,  I will demonstrate a way to do just that.

<!-- more -->

In their 2010 seminal work ["Continuous Delivery"](http://www.amazon.com/gp/product/0321601912?ie=UTF8&tag=martinfowlerc-20&linkCode=as2&camp=1789&creative=9325&creativeASIN=0321601912) [Jez Humble](http://jezhumble.net/) and [David Farley](http://www.davefarley.net/) described a maturity model for continuous delivery. The goal of this model was to assess the gap between where you are and where you want to be and help to define the steps you need to take to go there.

The model identifies six main area's of interest:

* Build management and continuous integration
* Environments and deployments
* Release management and compliance
* Testing
* Data management
* Configuration management


Each of these area's must be at a certain level to be able to achieve the benefits of continuous delivery. One of the key points for increasing your continuous delivery performance is to make well-balanced steps. It doesn't really help if your build management is top notch 100%, but you don't have any automated testing. Value comes when you increase the level of maturity evenly over all six focus area's.

{% img /images/maturity_model.png Visualize the level of maturity for the six interest area's %}

The picture shows a method to make these levels visual. This really helps in discussions with stakeholders in finding out where you are and where you need to go. Based on the graph above, you can see that it's best to work on improvements in data management and configuration management before you start to address other area's.

#What's the scale?

In the model, they describe the following 5 levels:

0. Regressive
1. Repeatable
2. Consistent
3. Quantitatively managed
4. Optimizing

These levels are loosely based on the levels defined by the [Capability Maturity Model](http://en.wikipedia.org/wiki/Capability_Maturity_Model) originally from the [Carnegie Mellon Software Engineering Institute (SEI)](http://www.sei.cmu.edu/). The higher the number the better you are.

##What's next?

In the [next blog post]({% post_url 2013-10-12-levels-of-maturity-for-continuous-deployment %}), I will dig deeper into the six main area's of interest.