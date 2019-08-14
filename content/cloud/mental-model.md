+++
title = "Mental Model"
date = 2019-08-14T10:48:24+01:00
draft = false
image = ""
comments = false # set false to hide Disqus
share = true	# set false to hide share buttons
author = "Mike"
weight = 700


[menu.main] 
    Name = "Mental Model" 
    identifier = "Mental Model"
    parent = "cloud"
+++

We can think of Cloud services in three levels:

* Service - a fully managed service, the easiest to use, but the least configurable, provides [Serverless]({{< ref "Serverless" >}}) offerings
* Platform - a semi-managed approach providing wizards, lots of configuration options for common use cases, but not complete control, often on a [PaaS]({{< ref "PaaS" >}})
* Infrastructure - building what you need yourself from [IaaS]({{< ref "IaaS" >}}), total control, but hardest to use

{{< figure src="/images/cloud_model.png" alt="Cloud Mental Model" class="img-800-center">}}

We can apply these levels to different aspects of Cloud computing such as compute, storage, AI etc. Generally speaking, using the higher-level offerings at the **Service** and **Platform** level will be quicker and easier than building everything up yourself from the [Infrastructure]({{< ref "IaaS" >}}) level.

When solving problems with cloud computing, start at the top, and only work downwards if you really have to. Start by asking:

* What native cloud service does this for me?
* What marketplace/serverless solution does this for me?