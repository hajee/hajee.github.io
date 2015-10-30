---
layout: redirect
title: "Asses YOUR continuous deployment maturity"
date: 2013-10-24 12:45:47
comments: true
categories: ['devops', 'visualize']
keywords: devops, visualize, maturity level, continuous deployment, continuous integration
description: This blog post describes the practices belonging to a certain maturity level.
redirect_to: https://www.enterprisemodules.com/blog/2013/10/asses-YOUR-continuous-deployment-maturity/
---
In the last couple of blog posts, I've talked about how to describe how mature you are in your ability to do continuous deployment. [This blog post]({% post_url 2013-10-02-visualize-your-continuous-deployment-maturity %}) introduced a way to visualise the maturity. In [this blog post]({% post_url 2013-10-12-areas-of-interest-to-realize-continuous-deployment %}) I described the area's of interest on the x-scale of the graph. While in [the last blog post]( {% post_url 2013-10-17-levels-of-maturity-for-continuous-deployment %}) I described the levels of maturity on the y-scale. That's all nice, but how do you use these ingredients to assess *YOUR* continuous deployment maturity? In this blog post,  I will introduce  some criteria.

<!-- more -->

["The book Continuous Delivery"](http://www.amazon.com/gp/product/0321601912?ie=UTF8&tag=martinfowlerc-20&linkCode=as2&camp=1789&creative=9325&creativeASIN=0321601912) [The book] contains the following matrix.

{% img /images/maturity-matrix.png The Continuous Deployment Maturity Matrix %}

This matrix helps to get a basic feel of what you need to do to get to a certain level of maturity in a specified area of interest. But it is still rather general. It the next few sections I will describe a set of practices that I feel, *need* to be filled in to claim this maturity level. I would really like to hear from you what kind of practices YOU think are needed.

## Build management

Build management are all processes and tools we need to ensure that,at any point in time, we can build a specific version of our software.

### To be repeatable you need:

* A build is done regularly. Preferable daily or at least weekly 
* The build is fully automated
* Every build is concluded with a unit-test
* The unit-tests test 70% or more of all business functionality 
* Every build retrieves the source from a source code management system

### To be consistent your need:

* Every change to the source control systems, triggers a new build and a new (unit-)test 
* All dependencies with other source packages and libraries are known and managed 
* All build and test scripts are being reused.

### To be quantitatively  managed, you need:

* Metrics of all builds are collected 
* The metrics of all builds are visual to the whole team 
* Improvement actions are described based on the build metrics 
* After a failure of the automated build, all activities are first directed at resolving the issues

### To be at an optimising level, you need:

* Teams frequently discuss integration problems and solutions 
* The team strives to better visibility of problems using automated solutions 
* The team strives to signalling the problems as early as possible using automated solutions

##Environments and deployment

To be able to do continuous delivery, there must be a pipeline of systems for doing DTAP(Development Testing, Acceptance and Production) like tests.

### To be repeatable you need:

* Automated deployment to some environments 
* Creation of environments is cheap (integration) 
* All configuration is externalized 
* All configuration is versioned

### To be consistent your need:

* Fully automated self-service push-button process for deploying software 
* Same process to deploy to every environment. 
* Scripts and tools are reused

### To be quantitatively  managed, you need:

* Orchestrated deployments managed 
* Release, and rollback processes tested.

### To be at an optimising level, you need:

* Provisioning fully automated
* Virtualization used if applicable

##Release management and compliance 
There must be a (strict) change management process including regulated approvals to go from state to state (e.g. from testing to acceptance and so on to production). These change management processes and approvals must be enforced.

### To be repeatable you need:

* Infrequent releases but reliable 
* Limited traceability from requirements to release.

### To be consistent your need:

* Change management and approvals process defined 
* Change management and approvals process enforced 
* Regulatory and compliance conditions met

### To be quantitatively  managed, you need:

* Environment  health monitored
* Application health monitored

### To be at an optimising level, you need:

* Operations and delivery teams regularly collaborate to manage risks 
* Operations and delivery teams regularly collaborate to reduce cycle time.

##Testing

Testing must be highly automated. You need at least automated unit-tests and a set of automated acceptance tests. It is preferable to have the acceptance test scenario's written by testers and business representatives in cooperation.

### To be repeatable you need:

* Tests are automated
* Tests are written during story development

### To be consistent your need:

* Automated unit-test  available
* Automated acceptance test available 
* Automated acceptance test are written with/by testers 
* Testing is an integral part of the development process

### To be quantitatively  managed, you need:

* Quality metrics and trends tracked 
* Non functional requirements defined 
* Non functional requirements measured

### To be at an optimising level, you need:

* Production rollbacks rare. (< 5%) * Defects found and fixed immediately. ( < 48 hr)

##Data management

You need to have automated the way you change your data model and also the configuration data inside the database.

### To be repeatable you need:

* Changes to databases done with automated scripts 
* Changes to databases are versioned with the application

### To be consistent your need:

* Database changes performed automatically as part of the deployment process

### To be quantitatively  managed, you need:

* Database upgrades tested with every deployment 
* Database rollbacks tested with every deployment 
* Databases performance monitored 
* Database performance continuous optimized

### To be at an optimising level, you need:

* release to release feedback loop of database performance and deployment process 
* release to release feedback loop of the deployment process

##Configuration management

To be able to get built every version in time at any moment, we need source code management tools like [git](http://git-scm.com/) or [subversion](Apache Subversion).

### To be repeatable you need:

* Version control in use for source code 
* Version control in use for build scripts * Version control in use deployment scripts 
* Version control in use for data migrations

### To be consistent your need:

* Libraries and dependencies managed 
* Version control usage policies determined by change management process

### To be quantitatively  managed, you need:

* Developers check-in to mainline at least once a day 
* Branching only used to release.

### To be at an optimising level, you need:

* Regular validation that CM policy supports effective collaboration 
* Regular validation that CM policy supports rapid development 
* Regular validation that CM policy supports auditable change management processes

##This leads to?
When you score all these assesments questions, and you plot them on the [graph]({% post_url 2013-10-02-visualize-your-continuous-deployment-maturity %}). You get the next graph.


{% img /images/maturity_model.png Visualize the level of maturity for the six interest area's %}
