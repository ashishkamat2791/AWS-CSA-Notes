# SQS

 ![Alt text](http://docs.aws.amazon.com/autoscaling/latest/userguide/images/sqs-as-workflow-diagram.png "SQA")

Oldest AWS Service
Gives you access to message queue that can be used to store messages while waiting for computers to process them
Distributed queue system that enables web service application to quickly & reliably queue message that on 
component in app generates to be consumed by another component.

queue is a temporary repository for message that are awaitinig processing.

```
Eg Meme website

If you loose Ec2 instnance, messages will remain overthere not going to loose, another EC2 instance will pick up that
```

```
Eg Travel Website
If application server crashes, message still remain in queue, marked as invisble, for Timeout window, after it outs, 
message will come again & anthoer app will pick up that job (2 times a message)
```

## Advanatages

1) **decoupling** component of application to run independently.
2) Any component of distributed app can store message in **fail safe** queue.

```
 Message can contain upto **256 KB** text in any format
queue act as buffer between component producing & saving data, & component receiving data for processing
queue resolves issue that arise in the producer is producing work faster than consumer can process it, 
or if producer/consumer are only intermittntly connected to the network
```

## Types of Queue

### 1) Standard Queue

unlimited transactions per second
gurantess message is delived **atleast once** 
however because of of highly available applications expecting **high throughput** same message might get 
deliverd **twice**

provide best effort ordering which ensures message are geerally delivered in same-way as they sent.

### 2) FIFO

Complemets Standard queue
most important feture is **FIFO** exactly once processing
order is preserved for sent and recived unless consumer process and delte it.
No duplications
supports message groups that allow multiple ordered message groups witihn a single queue 
limited to 300 transactions per second (TPS)
but have all capabilities of Standard one


## Key facts

1) Pull based not push based
2) Message is of **256 KB** in size (json,xml,txt)
3) Messages can be kept in queeue from **1** min to **14** days **deafult 4** days
4)Visiblity Time out** (same message twice) amount of time message is invisible in SQS queus after reader 
picks up that message. Provided job is processed before visibilty time out expires, message will then
be deleted from queue.
If job is not processed within time, message will be visible again & another reader process.
5) **Visibilty Time out** is max of **12** hrs
6) Gurantess that your message will be processed atleast once.


### Values

|Sr No|Parameter|Min Value|Max Value|Default value|
|--|--|--|--|--|
| 1 | Visibiity Time out| 0 sec| 12 hr|30 Sec|
|2| Message Rentention Period|1 min|14 days|4 days|
|3|Message size|1 KB|256 KB|256 KB
|4|Delivery delay|0 sec|15 minutes|0 seconds|
|5|Receive Message Wait time|0 sec|20 sec|0 sec|
## Types of Polling

### A] Long Polling (1-20 seconds)
Allows SQS service to wait untill a message is available in a queue before sending a response, and will return 
all messages from all SQS services.
Long polling **reduces API requests** (over using short polling)

### B] Short polling
SQS samples a subset of servers and returns message from just those servers
will not return all possible messages in a poll
Increase API requests (over long polling), which increase costs.

## SQS Workflow
* Generally a worker instance will "poll" a queue to retrive waiting message for processing
* Auto scaling can be applied based off queue size that if a component of your application 
has an increase in demand, the no of worker instance can increase.


## SQS vs SWF

| No | SQS | SWF
|--|--|--|
|1 API  are of|message oriented| task oriented
|2 Keeping track of all tasks| need to implement your own application-level tracking|managed by SWF
|3 Application focus| Need to implement on your own| Application-centric view that lets you search for executions, drill down into Its details
|4 Connectivity between tasks| Need to implement on you own| Provided by SWF, such as passing dat between tasks, and flexibity in distribution of tasks
|5 Workflows| Can build basic workflows| Provided by SWF out of the box