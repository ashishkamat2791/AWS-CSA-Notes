# Elasticity and Scalability

* *Proactive Cycle Scaling*: Scaling that occurs at the fixed interval.
* *Practive Event-based Scaling*: Scaling that occurs in anticipation of an event.
* *Auto-scaling based on demand*: Scaling that occurs based off of increase in demand of application

### Plan to scale out rather than up (Horizontal Scaling):

* Add more EC2 instances to handle increase in capacity rather than increasing in size.
* Be sure to design for proper instance size to start.
* Use tools like Auto scaling and ELB.
* A scaled service should be fault tolerant and operationally efficient.
* Scalable service should become more cost effective as it grows.

### DynamoDB is fully managed NoSQL service from AWS:
* With high availabilty and scaling already built in.
* All the developer has to do is specify required throughput for the tables.

### RDS requires scaling in a few differnt ways:

* RDS does not support a cluster of instances to load traffic across.
* Beacuse of this there are a few different methods to scale traffic with RDS:l
    * Utilize read replicas to offload heavy read only traffic.
    * Increase the instance size to handle increase in load.
    * Utilize ElasticCache clusters for caching DB session information

    


