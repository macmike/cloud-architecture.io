+++
title = "AWS S3 Lambda"
date = 2019-07-12T10:00:34+01:00
draft = false
comments = false # set false to hide Disqus
share = true	# set false to hide share buttons
author = "Mike"
layout = "tutorial"
weight = 600


[menu.main] 
    Name = "AWS S3 Lambda" 
    identifier = "aws-s3-lambda"
    parent = "tutorials"

+++



{{< tutorial_header "Introduction" "S3" "Lambda" "Security" "Coding" "Send to API" "Client">}}
 





{{< tutorial_section number="1" title="Introduction" description="We're going to make a simple serverless app" shownext="true">}}

{{< figure src="/images/tutorials/aws-s3-lambda/awss3lambda_arch.png" alt="Tutorial Architecture" class="tutorial_image">}}

The app will process text files, enriching them with sentiment analysis and key-phrase detection.

The app is going to made up of two S3 buckets: a source bucket where we'll upload text files and a target bucket which stores the processed data.

We'll process the data with a Lambda function that reads the file from the source bucket, calls the Comprehend service and then writes the results to a target S3 bucket.

As a bonus, you can send your processed data to an extra API to aggregate results!
     
**Important!** First check you can log into the AWS console, once you've logged in change the Region (in the top right) to `London` (eu-west-2)
{{< /tutorial_section >}}









{{< tutorial_section number="2" title="S3" description="Create two S3 buckets" shownext="true">}}

{{< figure src="/images/tutorials/aws-s3-lambda/awss3lambda_s3_create.png" alt="Create Buckets" class="tutorial_image">}}
1. In the AWS console, [go to S3](https://s3.console.aws.amazon.com/s3/home?region=eu-west-2#)

2. Create 2 buckets:
  * one for uploading text files
  * one for uploading storing the processed data

All S3 buckets must be uniquely named globally and follow DNS naming conventions, so call your bucket something like `<firstname>-demo-source`.

You can accept all of the other defaults for now.

{{< /tutorial_section >}}



