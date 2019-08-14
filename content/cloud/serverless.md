+++
title = "Serverless"
date = 2019-03-27T11:07:23Z
draft = false
image = ""
comments = false # set false to hide Disqus
share = true	# set false to hide share buttons
author = "Mike"
weight = 500

[menu.main] 
    Name = "Serverless" 
    identifier = "serverless"
    parent = "cloud"
+++

Serverless refers to a class of cloud services that require minimal or zero server management, configuration, patching, provisioning or scaling actions by the user.

The most common examples are in the compute space with "serverless functions" such as AWS Lambda, Azure Functions or Google Cloud Run where you can write code and have it respond to events without any management of cloud resources. To learn more about serverless computing, try [Tutorial: AWS S3 Lambda]({{< ref "aws-s3-lambda" >}})

Serverless doesn't just apply to short-lived compute though, it also applies to:

* Serverless container management and execution
* Databases (e.g. AWS DynamoDb, Azure CosmoDB)
* Storage (e.g. AWS S3, Azure Blob Storage)
* Other managed services such as AI, Search, Messaging, Queueing etc.