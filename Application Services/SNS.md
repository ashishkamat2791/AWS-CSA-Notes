# SNS

![Alt text](http://docs.aws.amazon.com/sns/latest/dg/images/sns-mobile-direct.png "SNS Service")

Web service that makes it easy to setup, operate and send notifications from the cloud. It provides developers with a highly scalable, flexible and cost effective capabilty to publish message from an application and immendiately deliver to subscribers or other application

Push based notifications to
* Mobile devices
* SQS
* Http endpoint
* **lambda function**

```
 invoked with the payload of the published message. It then receives the message payload as an input parameter and can manipualte the information in the message, to other SNS topics or AWS sevices. 
 ```


## Concepts

* **Publisher**- who is doing job
* **Subscriber**- who is receiving notification
* **Topic** - Actual concern

### End points:

* HTTP 
* HTTPS
* Email
* Emai-JSON
* SQS
* Application
* lambda

```
* Allows you to group multiple recipent using topic
* Access point topic allowing receipents to dynamically subscribe for identical copies of same notification.
* One topic can support to multiple end-point types
* When you publish once to a topic, SNS delivers appropriately formatted copies of your message to each subscriber.

* To prevent from messages being lostAll messages mto SNS are stored redundantly across multiple AZ.
```
### Benefits
* Instanteneous push based delivery (No polling)
* Simple API and easy integration with application
* flexible message delivery over multiple transport protocol
* Inexpensive pay-as-you go model
* Web-based AWS console point & click

 
