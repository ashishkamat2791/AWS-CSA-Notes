# ASG 



## Overview


* provides the ability to ensure a correct number of EC2 instances are always running to handle the load of the application
* helps to achieve better fault tolerance, better availability and cost management
* helps specify Scaling policies which can the be used to launch and terminate EC2 instances to handle any increase or decrease in demand on the application.

* Auto Scaling attempts to distribute instances evenly between the AZs that are enabled for the Auto Scaling group.

* It does this by attempting to launch new instances in the AZ with the fewest instances. If the attempt fails, Auto Scaling attempts to launch the instances in another Availability Zone until it succeeds


## ASG Main Components



### Launch Configuration


* template that an Auto Scaling group uses to launch EC2 instances.
* similar to EC2 configuration and involves selection of the Amazon Machine Image (AMI), the instance type, a key pair, one or more security groups, and a block device mapping.
* Launch configuration can be associated multiple Auto Scaling groups
*  can’t be modified after creation and needs to be created new if any modification required
* Basic or Detailed monitoring for the instances in the Auto Scaling group can be enabled when a launch configuration is created.
* By default, basic monitoring is enabled when you create the launch configuration using the AWS Management Console and detailed monitoring is enabled when you create the launch configuration using the AWS CLI or an API


### Auto Scaling Groups

```
core of Auto Scaling and contains a collection of EC2 instances that share similar characteristics and are treated as a logical grouping for the purposes of instance scaling and management.
```
It requires following things:

* **i) Launch configuration** 
to determine the EC2 template to use for launching the instance

* **ii) Minimum & Maximum capacity** 
to determine the number of instances when an autoscaling policy is applied. The number of instances cannot grow beyond this boundaries
iii) Desired capacity
to determine the number of instances the ASG must maintain at all times. If missing, it equals to the minimum size. 

**An Auto Scaling group’s desired capacity is the default number of instances that should be running. A group’s minimum capacity is the fewest number of instances the group can have running**

* **iv) Availability Zones or Subnets** 
in which the instances will be launched.

* **v) Metrics & Health Checks** 
 metrics to determine when it should launch or terminate instances and health checks to determine if the instance is healthy or not



### Working

* Auto Scaling group starts by launching a desired capacity of instances and maintains this number by performing periodic health checks.
* If an instance becomes unhealthy, it terminates and launches a new instance
* Auto Scaling group can also use scaling policies to increase or decrease the number of instances automatically to meet changing demands


### ASG with Launch Config

* Auto Scaling group can be associated with a single launch configuration.
* As the Launch Configuration can’t be modified once created, only way to update the Launch Configuration for an Auto Scaling group is to create a new one and associate it with the Auto Scaling group.
* When the launch configuration for the Auto Scaling group is changed, any new instances launched use the new configuration parameters, but the existing instances are not affected.


### Deletion

Auto Scaling group can be deleted from CLI, if it has no running instances else need to set the minimum and desired capacity to 0. This is handled automatically when deleting an ASG from AWS management console.



**Auto Scaling groups cannot span multiple regions.**

## Auto Scaling Plans



### Keep It as it is


* Auto Scaling ensures a steady minimum (or desired if specified) count of Instances will always be running.
* If an instance is found unhealthy, Auto Scaling will terminate the Instance and launch a new one
* Auto Scaling group determines the health state of each instance by periodically checking the results of EC2 instance status checks
* Auto Scaling marks an instance unhealthy and launches a replacement if
	- the instance is in a state other than running,
	- the system status is impaired, or
	- Elastic Load Balancing reports the instance state as OutOfService.
* After an instance has been marked unhealthy as a result of an EC2 or ELB health check, it is almost immediately scheduled for replacement. It never automatically recovers its health.

* When your instance is terminated, any associated Elastic IP addresses are disassociated and are not automatically associated with the new instance.
Elastic IP addresses must be associated with the new instance manually.

* Similarly, when the instance is terminated, its attached EBS volumes are detached and must be attached to the new instance manually


### Manual Scaling

 can be performed by
* Changing the desired capacity limit of the Auto Scaling group
* Attaching/Detaching instances to the Auto Scaling group

* Attaching/Detaching of an EC2 instance can be done only if
	* Instance is in the running state.
	* AMI used to launch the instance must still exist.
	* Instance is not a member of another Auto Scaling group.
	* Instance is in the same Availability Zone as the Auto Scaling group.
	* If the Auto Scaling group is associated with a load balancer, the 	instance and the load balancer must both be in the same VPC.

* Auto Scaling increases the desired capacity of the group by the number of instances being attached. But if the number of instances being attached plus the desired capacity exceeds the maximum size of the group, the request fails.

* If you detach an instance from an Auto Scaling group that is also registered with a load balancer, the instance is deregistered from the load balancer. If connection draining is enabled for your load balancer, Auto Scaling waits for the in-flight requests to complete.


### Schedule Scaling


* Scaling based on a schedule allows you to scale your application in response to predictable load changes for e.g. last day of the month, last day of an financial year
* Scheduled scaling requires configuration of Scheduled actions, which tells Auto Scaling to perform a scaling action at certain time in future, with the start time at which the scaling action should take effect, and the new minimum, maximum, and desired size the group should have
* Auto Scaling guarantees the order of execution for scheduled actions within the same group, but not for scheduled actions across groups
* Multiple Scheduled Actions can be specified but should have unique time value and they cannot have overlapping time scheduled 


### Dynamic Scaling


* Allows you to scale automatically in response to the changing demand for e.g. scale out in case CPU utilization of the instance goes above 70% and scale in when the CPU utilization goes below 30%
* Auto Scaling group uses a combination of alarms & policies to determine when the conditions for scaling are met.
	* An alarm is an object that watches over a single metric over a 	specified time period. When the value of the metric breaches the defined 	threshold, for the number of specified time periods the alarm performs 	one or more actions (such as sending messages to Auto Scaling).
	* A policy is a set of instructions that tells Auto Scaling how to 	respond to alarm messages.


##### Dynamic scaling process works as below (For Professioanal )

* 1) Amazon CloudWatch monitors the specified metrics for all the instances in the Auto Scaling group
* 2) Changes are reflected in the metrics as the demand grows or shrinks
* 3) When the change in the metrics breaches the threshold of the CloudWatch alarm, the CloudWatch alarm performs an action. Depending on the breach, the action is a message sent to either the scale-in policy or the scale-out policy
* 4) After the Auto Scaling policy receives the message, Auto Scaling performs the scaling activity for the Auto Scaling group.
* 5) This process continues until you delete either the scaling policies or the Auto Scaling group



### Multiple Policies

* An Auto Scaling group can have more than one scaling policy attached to it any given time.
* Each Auto Scaling group would have at least two policies: one to scale the architecture out and another to scale the architecture in.


### Default Termination Policy


* 1) Selection of Availability Zone
	- selects the AZ, in multiple AZs environment, with the most instances 	and at least one instance that is not protected from scale in.
	- selects the AZ with instances that use the oldest launch configuration, 	if there are more than one AZ with same number of instances
* 2) Selection of an Instance in the Availability Zone
	- terminates the unprotected instance using the oldest launch 	configuration, if one exists.
	- terminates unprotected instances closest to the next billing hour, If 		multiple instances with oldest launch configuration. 
  

### Auto Scaling Cool Down


* Auto Scaling cooldown period is a configurable setting for your Auto Scaling group that helps to ensure that Auto Scaling doesn’t launch or terminate additional instances before the previous scaling activity takes effect and allows the newly launched instances to start handling traffic and reduce load.

* When Auto Scaling group dynamically scales using a simple scaling policy and launches an instance, Auto Scaling suspends the scaling activities for the cooldown period (default 300 seconds) to complete before resuming scaling activities.


* When manually scaling the Auto Scaling group, the default is not to wait for the cooldown period, but you can override the default and honor the cooldown period.
* Note that if an instance becomes unhealthy, Auto Scaling does not wait for the cooldown period to complete before replacing the unhealthy instance.
* Cooldown periods are automatically applied to dynamic scaling activities for simple scaling policies and is not supported for step scaling policies.

### Auto Scaling processes 

includes

* 1) Launch – 
Adds a new EC2 instance to the group, increasing its capacity.
* 2) Terminate – 
Removes an EC2 instance from the group, decreasing its capacity.
* 3) HealthCheck -
Checks the health of the instances.
* 4) ReplaceUnhealthy – 
Terminates instances that are marked as unhealthy and subsequently creates new instances to replace them.
* 5) AlarmNotification – 
Accepts notifications from CloudWatch alarms that are associated with the group. If suspended,  Auto Scaling does not automatically execute policies that would be triggered by an alarm
* 6) ScheduledActions –
 Performs scheduled actions that you create.
* 7) AddToLoadBalancer – 
Adds instances to the load balancer when they are launched.
* 8)**AZRebalance**
Balances the number of EC2 instances in the group across the Availability Zones in the region.


### AZ Rebalancing

* If an AZ either is removed from the ASG or becomes unhealthy or unavailable, Auto Scaling launches new instances in an unaffected AZ before terminating the unhealthy or unavailable instances
- When the unhealthy AZ returns to a healthy state, Auto Scaling automatically redistributes the instances evenly across the Availability Zones for the group.


* If you suspend Launch, AZRebalance neither launches new instances nor terminates existing instances. This is because AZRebalance terminates instances only after launching the replacement instances.
* If you suspend Terminate, the ASG can grow up to 10% larger than its maximum size, because Auto Scaling allows this temporarily during rebalancing activities. If it cannot terminate instances, your ASG could remain above its maximum size until the Terminate process is resumed




### Instance Protection


* Instance protection controls whether Auto Scaling can terminate a particular instance or not.
* Instance protection can be enabled on a Auto Scaling group or an individual instance as well, at any time
* Instances launched within an Auto Scaling group with Instance protection enabled would inherit the property.
* Instance protection starts as soon as the instance is InService and if the Instance is detached, it loses its Instance protection
* If all instances in an ASG are protected from termination during scale in and a scale-in event occurs, it can’t terminate any instance and will decrement the desired capacity.


* Instance protection does not protect for the below cases
	- Manual termination through the EC2 console, the terminate-instances 	command, or the TerminateInstances API.
	- Spot instances in an Auto Scaling group from interruption



#### Standby State


* Auto Scaling allows you to put the InService instance in the Standby state during which the instance is still a part of the ASG but does not serve any requests. 
* This can be used to either troubleshoot an instance or update an instance and return the instance back to service


