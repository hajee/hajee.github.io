---
layout: post
title: "Puppet building blocks"
date: 2013-12-30 20:14:10 +0100
comments: true
categories: ['devops','puppet', 'method']
keywords: devops, puppet, continuous deployment, continuous integration
description: A description of the main Puppet building blocks
---

In this blog post,  I will look into Puppet and describe the building blocks Puppet uses.

In Puppet, you describe how your system should be configured by describing the artefacts available on the system. Per artefact, you describe it's detailed configuration. A configured system contains many artefacts. How can we structure these artefacts in such a way that it is readable, understandable and maybe usable by other (parts of) the organisation.

<!-- more -->

##The resource type
Generally a system consists of files, services, processes, packages and so on and so on. In the Puppet world, these are called resources. Resources are of a specified type. Lets say, for example, we want to make sure a configuration file is available on a unix system.  Besides being available, it should also contain the right content. With Puppet, we can do this by using the `File` type.

```ruby

file {'/application/config.xml':
  ensure	=> present,
  content	=> '<xml>just some config file</xml>',
}
```

besides the `File` type, there are types for managing `Users`, `Groups`, `Services` and so on. Actually Puppet has a lot of built-in types. If you look at [type documentation](http://docs.puppetlabs.com/references/latest/type.html) on the puppet site,you see a list of 48 built-in types.

{% img /images/list_of_types.png List of built-in types %}

A resource type is the smallest building block available in Puppet. Besides to the built-in types, Puppet has some other mechanism's to define structured sets of resources on a system. These are the `class` and the `defined resource`.

A resource type is the smallest building block available in Puppet. Besides to the built-in types, Puppet has some other mechanism's to define structured sets of resources on a system. These are the `class` and the `defined resource`. 


##The class
[The Puppet documentation for classes](http://docs.puppetlabs.com/puppet/2.7/reference/lang_classes.html) states:

{% blockquote %}
Classes are named blocks of Puppet code which are not applied unless they are invoked by name. They can be stored in
modules for later use and then declared (added to a node's catalog) with the include function or a resource-like syntax.
{% endblockquote %}

Quite some definition. In layman's terms, though a Puppet class is a way of structuring resources into a building block. The class [apache](https://forge.puppetlabs.com/puppetlabs/apache), for example, contains all resources needed to install, configure and run an apache https daemon on your system.


##The defined resource
[The Puppet documentation for defined types](http://docs.puppetlabs.com/puppet/2.7/reference/lang_defined_types.html) states:

{% blockquote %}
Defined resource types (also called defined types or defines) are blocks of Puppet code that can be evaluated multiple
times with different parameters. Once defined, they act like a new resource type: you can cause the block to be evaluated
by declaring a resource of that new type.

Defines can be used as simple macros or as a lightweight way to develop fairly sophisticated resource types.
{% endblockquote %}

As you can see in the definition, just like the `class`, the defined resource is a block of Puppet code. So they are both a means to structure your Puppet code and make building blocks of reusable resources. The difference between a `class`and a  defined type is that a `class`may only be applied to your system. A defined type however, is some sort of template that can be applied multiple times to your system.


##The custom type
While the `class` and the defined type can and are used to describe small configurable elements on a system, the custom type is designed to do just that. Puppetlabs new that they would never be able to build all the `types` needed to describe all systems. So instead they made sure, Puppet is extensible by making your own types. In fact, all built-in types are build using the same extension mechanism that is available for custom types.


##Next time
This concludes our small introduction into the Puppet building blocks. Next time I will dive into building your own custom resources.
