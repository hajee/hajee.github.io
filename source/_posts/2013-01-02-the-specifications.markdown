---
layout: post
title: "The specifications"
date: 2013-01-02 19:28:48 +0100
comments: true
categories: 
---
[Appdrones](http://www.appdrones.com) uses the specifications as a basis for all the work in the work packages. In this blog post and video we will introduce the Appdrones speciations system.

<!-- more -->


##Gherkin
The Appdrones specifications are based on Gherkin. Gherkin is is a Business Readable, Domain Specific Language that lets you describe software’s behaviour without detailing how that behaviour is implemented. Gherkin serves two purposes – documentation and automated tests. 

<iframe class="left-image" width="420" height="315" src="http://www.youtube.com/embed/oZr6l22R8p0" frameborder="0" allowfullscreen=""></iframe>

###A feature 
In Gherkin functionality is described in features. A feature is a description of some sort of functionality you need. Every Feature has the following elements:

```cucumber
Feature: Feature
description
 Narrative 
Scenarios
```

In the narrative you can write anything you want, but the best thing is to use the narrative to describe what the business value of the feature. You can do this by questioning why you need this feature. This is called “popping the why stack”. You describe the narrative in the following format: 
In order to have some business value

```cucumber
as a specific user
I want to do some stuff
```

###Scenarios
A feature can have one or more scenarios. A scenario describes a specific situation in your feature. Let me give you an example: In the video we enter the feature “Order Pastries”. Within the feature we have the scenario: new customer and the scenario returning customer. In both cases we need to do something else.

##Gradually build your specs 
Most of the times when you start with a new project, you just have a basic idea of the functionality you want. You start with just entering the high level features.  Later you can enter the scenarios.