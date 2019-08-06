+++
title = "AWS S3 Lambda"
date = 2019-07-12T10:00:34+01:00
draft = false
comments = false # set false to hide Disqus
share = true	# set false to hide share buttons
author = "Mike"
layout = "tutorial"
weight = 600
summary = "We're going to make a simple serverless app. The app will process text files, enriching them with sentiment analysis and key-phrase detection. The app is going to made up of two S3 buckets: a source bucket where we’ll upload text files and a target bucket which stores the processed data. We’ll process the data with a Lambda function that reads the file from the source bucket, calls the Comprehend service and then writes the results to a target S3 bucket."


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

```json
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
```

6. Select Review Policy

    *You'd get a warning if anything was wrong here, any errors in a policy mean that the policy grants no permissions!*

7. Give your policy a meaningful name e.g. `<firstname>-S3ReadSourceBucket`

8. Select Create policy	
                     
9. Add another inline policy to allow writing files to the target bucket
The only permission required is PutObject and you should restrict it to just the target bucket	


{{< /tutorial_section >}}







{{< tutorial_section number="5" title="Coding" description="Let's write the code!" shownext="true">}}

{{< figure src="/images/tutorials/aws-s3-lambda/awss3lambda_open_function.png" alt="Open the function" class="tutorial_image">}}


1. Go back to your Lambda function code

    Be wary, there are a couple of deliberate bugs in part of this **code**, if you get stuck ask for help, don't get frustrated! The steps with **bugs** are labelled so you'll know where there might be problems.
    
* You'll need to add some import statements to your function code:	

```python
import boto3, json                                     
```

* Work out which S3 object in the source bucket has triggered lambda

```python
s3 = boto3.resource('s3')
sourceKey = event['Records'][0]['s3']['object']['key'] 
sourceBucket = event['Records'][0]['s3']['bucket']['name'] 
print("s3 object: " + sourceBucket + "/" + sourceKey)               
```

* Read the uploaded file from S3 (**bug**)

```pythons3 = boto3.resource('s3')
obj = s3.Object(a_bucket, a_key) 
sourceText = obj.get()["Body"].read().decode('utf-8')               
```
                    
* Call comprehend to analyse the text (**bug**)

```python
comprehend = boto3.client(service_name='comprehend')
sentiment = comprehend.detect_sentiment(Text=sourceText, LanguageCode='en')
keyPhrases = comprehend.detect_key_phrases(Text=sourceText, LanguageCode='en')   
```
                    
* Build a new object that combines all of the data

    **Important!** Don't change this bit, the exact format is important for later.

```python
targetData = json.dumps({
    'sourceKey': sourceKey, 
    'sourceBucket': sourceBucket, 
    'sourceText': sourceText,
    'sentiment': sentiment,
    'keyPhrases': keyPhrases
})        
```
                    
* Write the results to the target bucket (bug)

```python
newObj = s3.Object(targetBucket, targetKey) 
newObj.put(Body=targetData)
print("processed data: "+ targetData)    
```

Test your code by uploading a small text file to the source bucket, via the AWS console.

You can see the output of your function in CloudWatch logs.
{{< figure src="/images/tutorials/aws-s3-lambda/awss3lambda_lambda_test_event.png" alt="Debug event" class="tutorial_image">}}
* Debugging your function

    Because there's some bugs it won't work at first. Instead of uploading a file every time you want to test your function, you can create a test event
    
* Use the Select a test event drop-down next to the Test button at the top of the Lambda page
  * Select `Configure Test Events`
  * Select `Amazon S3 Put` as the template event
  * Edit the `S3Bucket.Name`, `S3.arn` and `S3.object.key` fields to reference your bucket name and the name of the sample file you uploaded earlier
  * Give your test event a name
  * You can now re-run the effect of the file upload by just pressing the Test button
  
	

If it works then you should see a new file in your target bucket which you can open to see the resulting JSON.

{{< /tutorial_section >}}







{{< tutorial_section number="6" title="Send to API" description="Send the data to an external API" shownext="true">}}

I've exposed an API that you can send your data to, a lambda function will be triggered that will put the data into an ElasticSearch instance, updating the Kibana dashboard.

* Add some new import statements to the top of your function

``` python
import urllib
from botocore.vendored import requests
```

* Towards the bottom of your code, after you've created all of the target data, but before you've sent the lambda return status, add a the following to call the API at `https://api.cloud-architecture.io/sendToElasticSearch?`
    
    Don't forget to change your username from mike to your name in the first line!	 
   
``` python
userparam = 'user=mike'
encodedData = urllib.parse.quote_plus(targetData)
api = 'https://api.cloud-architecture.io/sendToElasticSearch?'
dataparam = '&data='+encodedData
api_response = requests.get(api+userparam+dataparam)
```

* To check that the API is responding properly, you can add some print statements and check the CloudWatch logs

``` python
  print("api code: " + str(api_response.status_code))
  print("api response: " + str(api_response.text))
```

**Congratulations!**

You've completed the workshop on the next page you can see the latest output of the api :)

{{< /tutorial_section >}}






{{< tutorial_section number="7" title="Client" description="Send a snippet" >}}

<script language="javascript">
    
    const APIurl = "https://api.cloud-architecture.io/processSnippet?user=client&snippet=";
    
    //upload to AWS and start looking for results
    function sendSnippet(){
        resultTimeout = 2000; //time before resetting form

        var snippetText = $('#snippetText').val();
        snippetText = encodeURIComponent(snippetText);

        var apiCall = APIurl + snippetText;
        console.log("calling: " + apiCall);                
        showSpinnyThing();

        $.get(apiCall, function(data) {
            //Got some data                    
            hideSpinnyThing();    
            console.log(data);   
            $('#snippetText').val("");
        });            

    }


    //show the spinny thing
    function showSpinnyThing(){
        $('#snippetText').fadeTo( "fast" , 0.2);
        $('#throbber_wrapper').show();
        $("#progress_text").html("thinking...");   
    }

    //hide the spinny thing
    function hideSpinnyThing(){
        $('#snippetText').fadeTo( "fast" , 1.0);
        $("#throbber_wrapper").hide();                                      
    }          
    
    function formatDate(date) {
      var hours = date.getHours();
      var minutes = date.getMinutes();
      var ampm = hours >= 12 ? 'pm' : 'am';
      hours = hours % 12;
      hours = hours ? hours : 12; // the hour '0' should be '12'
      minutes = minutes < 10 ? '0'+minutes : minutes;
      var strTime = hours + ':' + minutes + ' ' + ampm;
      return date.getDate() + "/" + (date.getMonth()+1 ) + "/" + date.getFullYear() + "  " + strTime;
    }
    
    //Getting latest snippets
    //called by template when the last tab is opened
    const LatestNum = 5;
    const LatestAPIurl = "https://api.cloud-architecture.io/getRecentESEntries?num="+LatestNum;
    function updateTutorialResults(){
        resultTimeout = 5000; //time before resetting form

        $.get(LatestAPIurl, function(data) {

            //Got some data
            console.log('Getting latest ES entries..');                    
            //console.log(data);             
            
            for (var i=1;i<LatestNum+1;i++){
               $("#snip"+i).empty();
               if (i<data.totalhits+1){
                    var item = data.hits[i-1]._source;
                    //console.log(item);
                    var aDateTime = new Date(item["@timestamp"]);
                    var aDateTimeText = formatDate(aDateTime);
                    $("#snip"+i).text(aDateTimeText + ": "+ item.username + ": "+item.sourceText);
               } else {
                    $("#snip"+i).text(i + " - none");
               }
            }
            
            UpdateResultsTimeout = setTimeout(function(){                        
                updateTutorialResults();
            },resultTimeout);
        });  
    }
</script>

<p>Latest snippets:</p>
<div id="latest_snippets" class="latest_snippets">
    <ul>
        <li id="snip1">1</li>
        <li id="snip2">2</li>
        <li id="snip3">3</li>
        <li id="snip4">4</li>
        <li id="snip5">5</li>
    </ul>
</div>
<div id="tutorial_form_wrapper">
     <center>        
        <form id="frmTextAnalysis">      
            <!-- other comments text box -->
            <p>Send some text directly to the API</p>      
            <textarea placeholder="some text" id="snippetText" name="snippetText" rows="4" class="roboText"></textarea><br/><br/>
            <!-- submit -->
            <div class="form_buttons">
                <div class="w3-btn w3-black">
                    <button type="button" class="w3-bar-item w3-button" onclick="sendSnippet()">Send</button>
                </div>
            </div>
            <br/>
        </form>
        <!-- throbber -->
    <div class="throbber_wrapper" id="throbber_wrapper" style="display:none">
        <div class="sk-cube-grid">
            <div class="sk-cube sk-cube1"></div>
            <div class="sk-cube sk-cube2"></div>
            <div class="sk-cube sk-cube3"></div>
            <div class="sk-cube sk-cube4"></div>
            <div class="sk-cube sk-cube5"></div>
            <div class="sk-cube sk-cube6"></div>
            <div class="sk-cube sk-cube7"></div>
            <div class="sk-cube sk-cube8"></div>
            <div class="sk-cube sk-cube9"></div>
        </div>       
        <div id="progress_text" class="very_good"></div>
    </div>
   </center>
</div> <!-- form wrapper -->
            
                

{{< /tutorial_section >}}
