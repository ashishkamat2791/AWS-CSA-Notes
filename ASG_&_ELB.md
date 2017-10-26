# ASG and ELB

![Alt_Text](https://media.amazonwebservices.com/blog/2014/elb_auto_scale_instances_2.png "ALSG with ELB")
## Using ELB & Auto Scaling

* makes it easy to route traffic across a dynamically changing fleet of 		EC2 instances
* load balancer acts as a single point of contact for all incoming traffic 	to the instances in an Auto Scaling group.

## Attaching/Detaching ELB with Auto Scaling Group


* Auto Scaling integrates with Elastic Load Balancing and enables to attach one or more load balancers to an existing Auto Scaling group.
* ELB registers the EC2 instance using its IP address and routes requests to the primary IP address of the primary interface (eth0) of the instance.
* After the ELB is attached, it automatically registers the instances in the group and distributes incoming traffic across the instances
* When ELB is detached, it enters the Removing state while deregistering the instances in the group.
* If connection draining is enabled, ELB waits for in-flight requests to complete before deregistering the instances.


## High Availabilty & Redundancy


* It is recommended to take advantage of the safety and reliability of geographic redundancy by using Auto Scaling & ELB by spanning Auto Scaling groups across multiple AZs within a region and then setting up ELB to distribute incoming traffic across those AZs.


## Health Check


* Auto Scaling, by default, does not replace the instance, if the ELB health check fails
* ELB health check with the instances should be used to ensure that traffic is routed only to the healthy instances
* After a load balancer is registered with an Auto Scaling group, it can be configured to use the results of the ELB health check in addition to the EC2 instance status checks to determine the health of the EC2 instances in the Auto Scaling group.


## Monitoring


* Elastic Load Balancing sends data about the load balancers and EC2 instances to Amazon CloudWatch. CloudWatch collects data about the performance of your resources and presents it as metrics.
* After registering one or more load balancers with the Auto Scaling group, Auto Scaling group can be configured to use ELB metrics (such as request latency or request count) to scale the application automatically
