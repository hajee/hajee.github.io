---
layout: post
title: "How to test systems installations"
date: 2014-01-13 20:14:10 +0100
comments: true
categories: ['testing', 'devops']
keywords: devops, puppet, continuous deployment, infastructure testing
description: How to test your systems installations
---
Just imagine yourself installing a Linux system with an Oracle database and a WebLogic application server. There are a lot of manual steps that have to be taken. A lot of commands to be typed and a lot of configurations to be set right in order to get the perfect system for the application. A lot of things can go wrong. You can miss a configuration setting. You can forget a command. Hopefully you get an error message because you did something wrong, but it can also turn out te be a silent error. One you only see after you have given the system to the application developers, or worse one that only comes out after the system is running in production and some load is put onto it. Hoe do we make sure a system is correct after the installation. In this blog post,  I will describe how we used Rspec to test out installations.

<!-- more -->

## How it's done mostly
In the area's of interest for continuous deployment, testing is a separate topic. Although testing  has become mainstream in regular software development, testing isn't really that mainstream when it comes to environments and deployments. Certainly not automated testing. Most of the times, the operations guy checks a couple of items on a checklist. Does the system boot well? Are there any error messages during the boot? Can I log in as root? Can I ping to the router? Can I connect to the database? All good tests, but hardly sufficient.

##It's quite big and complex
Actualy te be certain a system is installed correctly, is a rather complex and big task. There are numerous configuration files and settings. Every individual setting might cause the system to misbehave. Not only that, but the settings are also interrelated. Sometimes, if I change setting X, then I must also change setting Y. If for example I change the hostname of a Linux system, I might also have to change the hostname for the web server.

From research,  we know that the human brain is very powerful. But it lacks the capacity to see and manage a lot of intricate small little details. So even a very clever devops engineer can easily forget the extra change in setting Y after he changes setting X.

##how can we manage?
We could of course after an installation have QA check all settings. Because there are so many of the small little, but important settings, this would become a very labour intensive task. Not to mention a tedious and an error prone task. We need help. Just like in regular software development, we need to test our units with automated tests. The units can be the different kinds of settings. In the figure below you see an extract of running a unit-test for  a Linux installation.

{% img /images/rspec_output.png Part of an Rspec report on an installation %}


##What tools do we need?
The market for testing tools for regular software is crowded. A lot of good tools and frameworks exist for that kind of work. The market for testing tools for devops is a lot more dense. We decided to use [RSpec](https://relishapp.com/rspec) a tool mostly used in behaviour driven software development in the [Ruby world](https://www.ruby-lang.org/en/). We choose Rspec because of these reasons:

- After a small test, it really seemed to fit
- It is not only great as a test tool but even better as a communication tool (more on that later)
- It is open source and therefore we don't need any expensive license
- It has a large and vibrant user community
- Because we were aiming at using [Puppet](http://puppetlabs.com/puppet/puppet-enterprise), we needed Ruby on our systems anyway.

##Communication
One of the best things of RSpec is the clarity of its reporting. We noticed that the RSpec reports, where a means of discussion between the different stakeholders. In the past,  we'd have these vague discussions about a setting. Not all stakeholders new what the setting meant and why it was setup this way. After using RSpec, all of a sudden, we could pinpoint a certain setting and have a meaningful discussion about the reason of the setting and the actual value.

##How we use it?

Like I explained before, we are using the automated tests to check our settings. This means we mostly do checks on those sometimes we do a little bit more. For example, when we check the settings of the DNS resolver on a system, it is quite easy to extend the test to do a lookup and a reverse lookup to assess if it is really working.

On the other hand, if a new package solves a certain bug, it is easy to test if a certain version of that package is installed =, but quite hard to simulate the bug te check if it is actually solved. So we don't do that.

##Is the test sufficient?
**NO** definitely not. Just like the unit-tests of a regular application is insufficient. the RSpec tests are just a first kind of smoke test. But we noticed it is a very valuable one. After the RSpec tests are done, you still need acceptance and integration tests. Preferably with the application and all related middleware installed.

##Next...
In the next blog post I will explain how we have structured our Rspec code. 