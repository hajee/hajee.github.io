---
layout: redirect
title: "Area's of interest for continuous deployment"
date: 2013-10-12 21:25:10 +0100
comments: true
categories: ['devops','method', 'maturity model']
keywords: devops, continuous deployment, continuous integration, maturity, cmm
description: Describe the six area's of interest for realizing continuous delivery
redirect_to: https://www.enterprisemodules.com/blog/2013/10/areas-of-interest-to-realize-continuous-deployment/
---
In [my last blog post]({% post_url 2013-10-02-visualize-your-continuous-deployment-maturity%}), I showed a way to visualize the level of maturity for the six interest area's of continuous delivery. In this blog post,  I will dig deeper into what the areas of interest are.

<!-- more -->

##The area's of interest

###Build management and continuous integration
Build management are all processes and tools we need to ensure that ,at any point in time, we can build a specific version of our software. Besides being able to build it, we also need to ensure that is works. To do this, we need a set of (preferably automated) unit-tests. To be able, to quickly see the impact of source code changes, at least every night a build must be done.

###Environments and deployments
To be able to do continuous delivery, there must be a pipeline of systems for doing DTAP(Development Testing, Acceptance and Production) like tests. It is cheap (meaning automated) to get a new environment for testing. Systems provisioning and application deployments are all automated. Also, there needs to be a way to automatically roll back to a previous well known working system state.

###Release management and compliance

Besides all sorts of tooling stuff, processes must be in place. There must be a (strict) change management process including regulated approvals to go from state to state (e.g. from testing to acceptance and so on to production). These change management processes and approvals must be enforced.

###Testing

To be able to do continuous delivery, testing must be highly automated. You need at least automated unit-tests and a set of automated acceptance tests. It is preferable to have the acceptance test scenario's written by testers and business representatives in cooperation. Not only functional tests need te be automated, there needs to be some sort of mechanism te check non-functional requirements like, for example, response times

###Data management

While most automated installation scripts focus on provisioning the software. The data in the database is just as important. Therefore, you need to have automated the way you change your data model and also the configuration data inside the database.

###Configuration management

To be able to get built every version in time at any moment,  we need source code management tools like [git](http://git-scm.com/) or [subversion](Apache Subversion). All components needed to get the software working, must be under this regime of version control. This includes the libraries and all database changes.

