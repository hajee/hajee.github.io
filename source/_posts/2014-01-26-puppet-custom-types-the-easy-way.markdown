---
layout: redirect
title: "Puppet Custom Types, the easy way"
date: 2014-01-26 13:57:20 +0100
comments: true
categories: ['puppet', 'devops', 'ruby']
keywords: devops, continuous deployment, infastructure puppet, easy_type, ruby
description: The easy way to building Puppet Custom Types with easy_type
redirect_to:  https://www.enterprisemodules.com/blog/2014/01/puppet-custom-types-the-easy-way/
---
Robert scratched his head. How would he get a Puppet class to manage a complex resource on his systems? I guess I’ll have to make a Custom Type, he thought. But last time I looked into that, I noticed you need to know a lot about Puppet Internals. 

If you recognize this thought process, maybe it’s time to meet [easy_type](https://github.com/hajee/easy_type). Like the name says, easy type is designed to make it easy to build a Custom Puppet Type. In this article, we will introduce [easy_type](https://github.com/hajee/easy_type). We do this by taking you along on in the process of  making a Custom Type. In the process, we explain how `easy_type` actually makes it…… well easy to build a Custom Type. In the first part, we will show you how to get Puppet to see and index all your resources. In the next blog posts, we will enhance the Custom Type to be able to create, remove and modify existing resources.

<!-- more -->

*This article is changed at the 28th of October to refelect changes in `easy_type`*

##When to build a Custom Type

Well that’s an interesting question! The Puppet language is actually very versatile, and you can do anything with it. But why would you step out of puppet and into ruby to build a Custom Type? In one of his [excellent blog posts](http://garylarizza.com/blog/2013/11/25/fun-with-providers/), Gary Larizza explains it in one sentence: “Because 20 execs in a defined type… “. Another indication, you’d be better of on a Custom Type path instead of a defined type, is when you need to build one or more custom facts. 

{% blockquote Gary Larizza in Fun With Puppet Providers%}
What would drive someone to write a custom type and provider for Puppet anyhow? Afterall, you can do ANYTHING IMAGINABLE in the Puppet DSL*! After drawing back my sarcasm a bit, let me explain where the Puppet DSL tends to fall over and the idea of a custom type and provider starts becoming more than just an incredibly vivid dream:

<ul>
	<li>You have more than a couple of exec statements in a single class/defined type that have multiple conditional properties like ‘onlyif’ and/or ‘unless’.</li>
	<li>You need to use pure Ruby to manipulate data and parse it through a system binary</li>
	<li>Your defined type has more conditional logic than your pre-nuptual agreement</li>
	<li>Any combination of similar arguments related to the above</li>
</ul>
If the above sounds familiar to you, then you’re probably ready to build your own custom Puppet type and provider. 
{% endblockquote %}

##Let’s get started

To get started, you first need to install `easy_type`. You can either add it to your `Puppetfile` or use the puppet module installer to install it. 

###Install `easy_type` using puppet-librarian

To add it to your `Puppetfile`, you can add the following line:

```ruby
mod "hajee/easy_type", :git => "git://github.com/hajee/easy_type.git"
```

After that run the librarian to add the right modules to your puppet tree:

{% img /images/easy_type_added.png easy_type added to modules %}


```sh
librarian-puppet install
```

The `librarian` reads the `Puppetfile` and puts the nescecary files into your module tree. After this command, you can see `easy_type` in your  list of modules.

###Install using puppet module installer.

To install `easy_type` using the puppet installer, enter the next command:

```sh
$ puppet module install hajee/easy_type
```

Well that was easy. Now we have all the basic requirements in place to start. What better time then now to think about the resource you want to manage.

##How to manage the resource?
Because `easy_type` hides some of the Puppet intricacies from you, you can focus on the resource. To continue, you need to know how: 

-	get a list of all available resources? 
-	what’s important in a resource?
-	to create a resource?
-	to modify an existing resource
-	to remove one

This is the basic information you need to build a custom resource.

#An example please?

As an example I’ve picked the same Custom Type as is described in the book [“Puppet Types and Providers"](http://shop.oreilly.com/product/0636920026860.do).  This is an excellent book if you are into writing custom resources. It describes in great detail everything you must known and do to build a Custom Type in the standard puppet way. In the book they state:

{% blockquote Puppet Types and Providers By Dan Bode, Nan Liu %}
the `custom_package` type is not intended to serve as a replacement of Puppet’s existing package type. It serves as an example of how to take advantage of the features of the type and provider APIs.
{% endblockquote %}

Of course, the same thing counts over here.

##A scaffold
To get started, it would be helfull if we have a scafffold. Let's say we want to name our own module `my_own_easy_type` and we name our own Custom Type `custom_package`. `easy_type` also contains some generators to make this easy. But first we have to create the directories and files needed for any puppet module:

```sh
$ puppet module generate robert-my_own_easy_type
```


Now we can start creating the custom type:


```sh
$ puppet type scaffold easy_type custom_package --force
```


##It works.... Well, kind of
Actually this is all you have to do to get the basic Puppet stuff in order. Now you can give the puppet command to get a view of all available resources:

```sh
puppet resource custom_package
```

And it shows..... nothing. No output. But what is more import at this stage, is no error's or warnings. Now we can start working on the thing we know best. How to get the information about our resource, a package in this example, out and manageable.

##Let's get the index of all packages
So let's change the `custom_package` so we can use Puppet to get a list of all resources. To do this, we need to add just a couple of lines. Lets first look at the method `to_get_raw_resources`. Its function is to return an Array containing all available resources you manage. Every Array entry is preferably a Hash. A Hash that contains the all the individual properties and parameters of an instance of your resource.

In our example,  we are managing packages. To get a list of packages on a Linux system, you can use the `rpm` command. The following os command returns a list of all packages formatted in a comma separated way containing its name and its version.

```sh
rpm -qa --qf '%{NAME}, %{VERSION}\n'
```

We would like the Custom Type to execute this command and convert the data to an Array of Hashes.

To do just that, we need to change the `to_get_raw_resources` method to:

```ruby
    to_get_raw_resources do
      packages_string = rpm('-qa','--qf','%{NAME}, %{VERSION}\n')
      convert_csv_data_to_hash(packages_string,['name', 'version'])
    end
```
The `packages_string` will contain a string with all the information. The `convert_csv_data_to_hash` method will convert it to a hash. The elements in the hash are named `name` and `version`.

To let `easy_type` know rpm is an os command, we need to add the line:

```ruby
set_command(:rpm)
```

##TA TAAHH

Now when we ask Puppet for the available `custom_packages`, we get a list of all the available packages.

```sh
puppet resource custom_package
```
Output:
```ruby
custom_package { 'GConf2':
  ensure  => 'present',
}
custom_package { 'MAKEDEV':
  ensure  => 'present',
}
...
```
But wait, didn't we also collect the version information? What about that? To Add the version information, we need to add a version property. A property looks very similar to the parameter that was already available in the scaffold. `Easy_type` contains a generator to add a property. Let's run it:

```sh
$ puppet type generate property version custom_package
```

Now when we ask Puppet for the available `custom_packages` again, we get a list of all the available packages, inclusing the version information.

```sh
puppet resource custom_package
```
Output:

```ruby
custom_package { 'GConf2':
  ensure  => 'present',
  version => '2.14.0',
}
custom_package { 'MAKEDEV':
  ensure  => 'present',
  version => '3.23',
}
...
```

##Next...
In the [next blog post]({% post_url 2014-02-08-puppet-custom-types-the-easy-way-part-2 %}), we will enhance our work. We will add support for changing existing resources. If, in the meanwhile you want to check `easy_type` out. You can checkout the source in the [github repository](https://github.com/hajee/easy_type). You can also check some [Oracle Custom Types](https://github.com/hajee/oracle) which are build upon `easy_type`. We would love to hear your feedback on this work. You can find the example [here](https://github.com/hajee/my_own_easy_type)

_Since first publication, some changes where made to the code fragments in this blog post. If you used the code in this post, please check the changes in the github repo_