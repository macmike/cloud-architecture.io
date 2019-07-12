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







{{< tutorial_section number="3" title="Lambda" description="Create a Lambda function" shownext="true">}}

{{< figure src="/images/tutorials/aws-s3-lambda/awss3lambda_create_function.png" alt="Create a function" class="tutorial_image">}}

1. In the AWS Console, [go to Lambda](https://eu-west-2.console.aws.amazon.com/lambda/home?region=eu-west-2#/functions)

2. Create a new function
  * Select `Author from scratch`
  * Call your function something you'll recognise, e.g. `<firstname>-processFile`
  * Choose `Python 3.x` as the runtime to be able to use the code snippets provided
  
    If you expand the `Permissions` item, you'll see the default is to `Create a new role with basic Lambda permissions` for your function - that's a good thing! 
    
    We'll edit the role later.	

3. Add a trigger that invokes your function by selecting S3 on the right under `triggers` in the `Designer`

4. Configure the S3 trigger to fire off new files being added to your *source* bucket

5. Make sure you click `Add` on the trigger configuration	

6. Scroll down past your code to the Basic Settings section. Change the Timeout to 6 seconds

7. Save your lambda function
(the orange button, top-right)

{{< /tutorial_section >}}










{{< tutorial_section number="4" title="Security" description="Configure Security Properly" shownext="true">}}

{{< figure src="/images/tutorials/aws-s3-lambda/awss3lambda_s3_read.png" alt="S3 Read policy" class="tutorial_image">}}

At the moment our Lambda function doesn't actually have enough rights to read from our source bucket or write to our target bucket. To give it permissions we need to edit the Execution Policy that was automatically created in the previous step.

In the AWS Console, go to IAM and select Roles

2. Find the execution role for your function 

    *It will be named the same as your function with a random id after it, e.g. `bob-processFile-role-diqmuuv6`*

3. We need to add 2 inline policies:
  * One to read from the source bucket
  * One to write to the target bucket
  
4. To add permissions, select Add inline policy and use the wizard to select:
  * `S3` as the service
  * `GetObject` as the allowed action
  * `<firstname>-demo-source` as the specific bucket
  *  `*` to allow reading any object within the bucket
  

5. Select the JSON view of the policy, it's actually quite simple, it should look very similar to this:
  
    *The only difference should be your bucket name*

{{< tutorial_codebox json>}}
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "VisualEditor0",
            "Effect": "Allow",
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::my-source-bucket/*"
        }
    ]
}
{{< /tutorial_codebox >}}

6. Select Review Policy

    *You'd get a warning if anything was wrong here, any errors in a policy mean that the policy grants no permissions!*

7. Give your policy a meaningful name e.g. `<firstname>-S3ReadSourceBucket`

8. Select Create policy	
                     
9. Add another inline policy to allow writing files to the target bucket
The only permission required is PutObject and you should restrict it to just the target bucket	


{{< /tutorial_section >}}







{{< tutorial_section number="5" title="Coding" description="Let's write the code!" shownext="true">}}

{{< figure src="/images/tutorials/aws-s3-lambda/awss3lambda_open_function.png" alt="Open the function" class="tutorial_image">}}

{{< /tutorial_section >}}







{{< tutorial_section number="6" title="Send to API" description="Send the data to an external API" shownext="true">}}

I've exposed an API that you can send your data to, a lambda function will be triggered that will put the data into an ElasticSearch instance, updating the Kibana dashboard.

{{< /tutorial_section >}}






{{< tutorial_section number="7" title="Client" description="Send a snippet" shownext="true">}}


{{< /tutorial_section >}}
