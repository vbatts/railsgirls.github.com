---
layout: default
title: Rails Girls on OpenShift
permalink: openshift
---

# Put Your App Online With OpenShift

*Created by Vincent Batts, [@vbatts](https://twitter.com/vbatts)*

### Get OpenShift

First you will need to have an OpenShift.com account, and stand up an application. 
On the OpenShift [get started](https://www.openshift.com/get-started) page to
sign-up, access the console for creating an application and to learn about
installing and using the the `rhc` tool.

__COACH__: Talk about the benefits of deploying to cloud/PaaS vs traditional servers.

### Preparing your app

#### Version Control

`git` is the most commonly used version control system used. Once you have
created the new rails application from the curriculum (e.g. `rails new myapp`)
then it will need to have git initialized for this application code.

From the base director of your new application (e.g. `cd myapp`), you can run
`git init` to initialize git for this application, but has not added any of your
code to it. 
We need to instruct git to ignore a couple of paths, that ought not be preserved.

{% highlight sh %}
git init
echo "public/uploads" >> .gitignore
echo "tmp" >> .gitignore
echo "logs" >> .gitignore
{% endhighlight %}

Lastly we add out application code to git and commit it.

{% highlight sh %}
git add .
git commit -m "initial commit"
{% endhighlight %}


#### adding openshift

Once you have started your new application code, git and have created an OpenShift,
then we are ready to add the OpenShift git as a 'remote' for our new application
code. To do this, from the root directory of our new application,
we will take the address for the openshift git repo (with _your_ unique address):

{% highlight sh %}
git add remote openshift ssh://1234567890deadbeef@myapp-mynamespace.rhcloud.com/~/git/myapp.git/
git fetch openshift
{% endhighlight %}

Since this pulls down a ready to use ruby application, we need to put our
application in its place. To do that run the 

{% highlight sh %}
git checkout -b tmp openshift/master 
git rm config.ru
git commit -m "remove the openshift config.ru"
git checkout master
git merge -m "Merging the OpenShift remote" tmp
git branch -D tmp
git push -u openshift master
{% endhighlight %}




