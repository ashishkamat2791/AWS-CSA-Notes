# Lambda

![Alt_Text](https://image.slidesharecdn.com/rigadevday-160302153204/95/riga-dev-day-lambda-architecture-at-aws-26-638.jpg?cb=1456933179 "Lambda")
* region specific
* Released in 2015

## It Encapsulate 
* data centres
* hardware
* assembly code/protocols
* high level languages
* Operating systems
* Application layer/AWS APIs


## Lambda can be used for


*  Compute Service where you can upload your code and create Lambda function.
  AWS lambda takes care of provisioninig and managing the servers that you use to run the code. You dont have to worry about Operating     Systems , patching, scaling etc. You can use Lambda in following ways

Eg 
```
So lets say we have got our user and our user wants to create MEM so they upload this to MEME to S3. Now since we have uploaded MEME to S3 It triggers an EVENT which is lambda function which might takes MEME and text we have supplied with it perhaps and then basically encode over the image and then store the image in S3
This lambda event might trigger another lambda of it which returns imahe location of the new file back to the user 
might then trigger another lambda event which will then take the image thats ins this s3 bucket and copy across another region somewhere else in the world
You could send this information to SQS or SNS which then goes to or trigger further events
lambda is scale out so it gives same consistency and throughput whether it is working for 1 user or millions of user. no need to worry about maintaining Infrastructure, load balancers
```

* As an event driven compute service where AWS lambda runs your code in response to events.These events could be changes to data in an Amazon s3 bucket or an Amazon DynamoDB table.
As a compute service to run your code in response to HTTP requests using API gateway or API calls made using AWS SDKs.

Eg
```
We have user browsing Google websites hits our server which goes to API gateway which triggers a lambda function Eg user wants to see discussion forum so lambda do computing and returns response back to user

Since lambda scales out automatically througput remains same among all users.
Everyime you are invoking API gateway cretes new lambda function so code is identical 
```

* Very good compared to EC2 service as we need to manage load balancing apply launch configurations do autoscaling etc


## Scale up vs Scale out

### Scales up
increase amount of resources like RAM, CPU

### Scale out
adding more instances to manage load

Lambda scales out efficiently


### language support as of now

* java
* node js
* c#
* python

### Pricing

* based on no of requests
* First 1 million request free then $0.20 per 1 million requests thereafter


### Duration

* duration is calculated from the time your code begins execution untill it returns or otherwise terminates, rounded up to nearest 100ms
* price depends on amount of memory allocated to your function
-* charged for $0.00001667 for every GB-second used


Cool!!

* No servers
* Continous Scaling
* super super super cheap

Exam Tips

*  out(not up) automatically
* functions are independent, 1 event = 1 function
* Lambda is serverless
* know what services are serverless (s3, api gateway, alexa, lambda)
* Lambda function can trigger another lambda functions, 1 event can= x functions if function trigger other functions

* Architecture can get complicated, AWS X-ray service allows to debug what is happening
* Lambda can do thing globally, you can use it back up s3 buckets to other S3 buckets etc.

* know your trigger
**all new triggers will be available in northen-virginea**


### Following are triggers available


* API Gateway
* AWS IoT
* Alexa 
* Clodfront
* Cloudwatch events
* Codecommit
* DynamoDB
* Kinesis
* S3
* SNS



**lambda duration time is max of 5 minutes**


