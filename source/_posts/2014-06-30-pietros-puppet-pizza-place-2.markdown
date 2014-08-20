---
layout: post
title: "Learning Puppet at the Puppet Pizza Place part 2"
date: 2014-06-30 15:00:15 +0200
comments: true
categories: ['puppet', 'devops', 'learning']
keywords: devops, continuous deployment, infastructure puppet, learning
description: Learning Puppet at the Puppet Pizza Place
---
#Learning Puppet at the Puppet Pizza Place

In this set of blog posts, I will teach you the base concepts of the [puppet DSL](http://puppetlabs.com/puppet). Most of the time Puppet is taught within the context of IT configuration management. I've chosen not to do so. I've chosen baking pizza's as the learning environment. It helps less technical people, like IT managers, for example, to get the concepts of Puppet. Checkout part 1 of the series [here]({% post_url 2014-06-26-pietros-puppet-pizza-place-1 %}))

<!-- more -->

## More pizza's....

Last time Pietro experimentented with Miss Piggy the pizaa backing robot. He used the Puppet DSL to describe a pizza Napolitane. After some experimenting, he'd got his first real pizza from Miss Piggy. That was all really nice, but Miss Piggy would really become an asset if Pietro was able to reuse the description of his pizza Napolitane.

##Puppet classes
Pietro looked in the Puppet manual and saw that Puppet had a mechanism for putting related ingredients together and resuing them. It was called a `class`. That was exactly wat he needed. Because a pizza in fact is nothing else then putting the right ingredients in the right order together with the right steps. So Pietro started with a class for 

##Puppetizing the menu card