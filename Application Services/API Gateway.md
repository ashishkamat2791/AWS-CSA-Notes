# API Gateway

Fully managed service that makes it easy fo developers to publish, maintain, monitor and secure APIs at any scale.
 With a few clicks in the AWS Managment console, you can create an API that act as front door for application to access data, business logic, or functionality from your backend services, such as application running on EC2, code running on AWS lambda, or any  web application

Eg Acloudguru Webiste

```
Users make request which calls API gateway which will trigger Lambda function or EC2 instance
```
## Features

## API Caching

speed up response rate by doing caching your endpoint response. with caching, you can reduce the no of calls made to your end point and also improve the latency of the requests to your API. When you enable caching fo a stage, API gateway caches response from end-point for specified time-to-live period in seconds, API gateway then responds to the requests by looking up the endpoint response from cache instead of making a requset to your endpoint.

## Monitoring
Cloudwatch can be used to monitor API gateway activity and usage
Monitoting can be done on API stage level
Throttling rules are monitored by Cloudwatch
Monitoring metrics include such statistics as:
* Caching
* Latency
* Detected Hosts
* Method level metrics can be mounted
**You can create Cloudwatch alarms based on these metrics**

## Cloudfront
* API gatway benefits from using Cloudfront
* have built in DDOS attack protection and mitigation
* All cloudfront locations become entry points to your API into your back-end
* Benefits are reduced latency and improved protection



### What It can do?
* Low cost and efficient
* Scales Effortlessly
* You can throttle Requests to prevent attacks


## same origin policy
Its a concept in Web application security model. under the policy, a web browser permits scripts contained in a first web page to access data in a second web pge, but only if both web pages have same origin.

## CORS Cross Origin Resouce sharing
on way at the other end can relax the same-origin policy.
Its a mechanism that allows restrictedresources on a web page to be requested from another domain outside the domain from which first is served.

## Exam Tips
* API gatway has caching capablities to increase performance
* low cost and scales automatically
* log rsults to cloudwatch
* AJAX/Javascript make sure that you have enabled CORS on API gateway

## Benefits

* Abilty to cache API response
* DDOS protection via cloudfront
* SDK generation for iOS, Android and Java script
* Supports Swagger for API dev tools Documentation
* Request/Response data transformation

