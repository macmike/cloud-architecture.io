+++
title = "About"
date = 2019-03-28T14:13:18Z
draft = false
image = ""
comments = false # set false to hide Disqus
share = true	# set false to hide share buttons
menu = "main"
author = "Mike"
weight = 600
+++

### How does it work

[cloud-architecture.io](https://cloud-architecture.io) is written using as [markdown](https://en.wikipedia.org/wiki/Markdown) on [github](https://github.com/macmike/cloud-architecture.io).

As content is pushed to github the [AWS Amplify](https://aws.amazon.com/amplify/) service picks up the changes, spins up a container to do the hugo build and deploys the site through the AWS content delivery network. This is all serverless and invisible, Amplify takes care of it all automatically providing a CI/CD pipeline for this site.

### Contributor Hall of Fame

{{< contributor 
   name="Mike MacDonagh"
   twitter="mikemacd" 
   blog="mikemacd.wordpress.com" 
   linkedin="mikemacdonagh" >}}


### Soft-Practice Ltd.

The site is run by [Soft-Practice Ltd.](https://soft-practice.com) a UK-based Cloud, Cyber & Agile Consultancy company for the good of the development community.
