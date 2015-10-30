---
layout: redirect
title: "Puppet Custom Types, the easy way (part 2)"
date: 2014-02-08 13:57:20 +0100
comments: true
categories: ['puppet', 'devops', 'ruby']
keywords: devops, continuous deployment, infastructure puppet, easy_type, ruby
description: The easy way to building Puppet Custom Types with easy_type (part 2)
redirect_to:  https://www.enterprisemodules.com/blog/2014/02/puppet-custom-types-the-easy-way-part-2/
---
In the [last blog post]({% post_url 2014-01-26-puppet-custom-types-the-easy-way %}), we started with our own custom type. We added the `easy_type` module, created the files necessary for getting started and got our custom running without any errors. We then added two lines to get into a state where Puppet was able to do an inventory of our systems. But a custom type not able to create, delete or modify the state of your system, wouldnt be very helpful. So in the blog post we are going to add that functionality to our custom_package type.

<!-- more -->

##Let's recap
Let's first look back at what we did last time. To get started with [easy_type](https://github.com/hajee/easy_type), we made sure `easy_type` is installed in the module path. We used `librarian-puppet` to get `easy_type` installed. After that,  we created the right directories and created a scaffold. Since the last blog post,  we have added the scaffold to the `easy_type`. This makes's it even easier to get started. To get it, use the next command:

```sh
cp -Rv easy_type/scaffold custom_package/lib/puppet
```

After we created the scaffold, we checked what puppet would do with the type and noticed `Puppet` didn't do anything, but also didn't complain. So a good start.

Then we added the 2 lines of code for getting the raw package information from the system. After that,  we added the 1 line of code that picked the name and version information from the raw package information. Then we had a working Puppet custom type. 

{% img /images/custom_package_list.png Index from custom_package %}

Wel working...Sort of. Because the type doesn't know yet how it can create, delete and modify resources. So that's what we're going to do next.

##How to create a resource in real life?
Like I said in the [last blog post]({% post_url 2014-01-26-puppet-custom-types-the-easy-way %}), a design goal of `easy_type` is to let you focus on the resource knowledge and let us do the Puppet stuff. So what is needed to create a new `custom_package` instance. To create a new `custom_package` instance, we need to install a package.

For `easy_type`,  it would be the easiest thing if we could use the same base command as we used to get an index. That would be the `rpm` command, but in this case the best way to install a package is a `yum` command.

```sh
yum -q install a_package
```

This would install the latest version. But what if we needed a specific version? Then `a_package` needs to be both the name and the version number, concatenated with a dash. For example:

```sh
yum -q install php-5.2.6-2
```

Will install php version 5.2.6-2

##And how to do it in the Puppet world?
So how do we get this knowledge into our own custom type? First we have to add the extra command (`yum`) that is used. We do this by changing the `set_command` line to:

```ruby
set_command [:rpm, :yum]
```

This line tells `easy_type` that we use `rpm` and `yum` as commands. Next we have to tell `easy_type` to use `yum` when we need to create a resource:

```ruby
on_create do |command_builder|
  command_builder.add do
    yum "install -y #{name}"
  end
end
```

But wait. What about the version number? Don't we need to do add it somewhere? And you are right. We need to add it at the definition of the property. At the property add the lines:

```ruby
on_apply do |command_builder| 
  command_builder.append do
    "-#{version}"
  end
end
```

The method is only run when we need to create a resource or when the attribute value in the manifest is different from the attribute value on the system. So in this case, because we create a resource the method is called. With the `append` method, we tell the `command_builder` to add some text to the string created before by the `command_builder.add`.

So now we are able to create a `custom_package` resource.

{% img /images/custom_package_created.png Install a package using custom_package type %}

##And now some destruction
Like we saw before, `yum` is the command used to install a package. `yum` is also used to uninstall a package and therefore delete a resource in the Puppet world. The command will be:

```sh
yum -q erase a_package
```
To get this wisdom into our custom type, we need to add some code to the `on_destroy` handler.

```ruby
on_destroy do | command_builder|
  command_builder.add do
    yum "erase -y #{name}"
  end
end
```

So besides indexing and creating, now our custom type is also ready for to destroy a resource.

{% img /images/custom_package_destroy.png Install a package using custom_package type %}

##How about modifying?

Like we did before, we want to focus on our knowledge of the resource. What do we do when we modify the version attribute? 

{% blockquote Just like in the book Puppet Types and providers%}
The on_modify handler is a naive implementation that does not handle downgrade properly. The correct implementation should compare against the installed software version and invoke package downgrade when appropriate. The code here is kept simple; for more complete examples, see the ~/src/puppet/lib/puppet/provider/packages directory.
{% endblockquote %}

So in our simple case, we just install the specified version. Actually we just do an `on_create`. So let's tell our type to behave like that.

```ruby
on_modify do | command_builder|
  on_create(command_builder)
end
```

So now when we change the version number, a different package is installed.

{% img /images/custom_package_modified.png Install a package using custom_package type %}

## AND TA TAAHH
Now we are ready. We have a Custom Puppet Type that has the ability to:

* Do an index
* create a new resource
* destroy/delete a resource
* and modify an existing resource

If we don't count the  boiler plate code, then we added just 18 lines of code to get this working. Not to bad.

##There's a lot more
Like I said in the introduction, this is really a simple example. Real life custom types are more difficult. So `easy_type` has some more functionality that is not shown in this examples. 

* support for standard mungers
* support for standard validators
* A lot of tricks in the command_builder so it's easy to build commands based on what Puppet thinks, needs to be done.
* support for extracting the definition of attributes and properties

If you would like to see more about `easy_type`, just let me know and I will see if we can do some more posts about it. For now, check the example source in the [github repository](https://github.com/hajee/my_own_easy_type). You can also check some [Oracle Custom Types](https://github.com/hajee/oracle) which are build upon `easy_type`. 

