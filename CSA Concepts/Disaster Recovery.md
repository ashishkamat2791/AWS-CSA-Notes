# Disaster Recovery

*Business disaster recovery key words: Very IMP for AWS CSA Exam*

*Recovery Time Objective (RTO)* : Time It takes after a disruption to restore operations back to its regular service level, as defined by the companies operational level agreement. (If the RTO is 4 hrs, you have 4 hrs to restore service back to anacceptable level)

*Recovery Point Objective*: Acceptable amount of data loss measured in time. (i.e If the ssytem goes down at 10 pm and RPO is 2 hrs, then you should recover all data as part of application as it was before 8PM)


*The AWS Services should be determined based off the the business RTO and RPO*

*Pilot light*: A minimal version of your product environment that isrunning on AWS. This allows replication from on-premise servers to AWS, and in the event of disaster the AWS environment spins up more capacity (elassticty/configuration) and DNS is switch from on-premise to AWS. It is impotant to keep up to date AMI and instacne configurations if following pilot light protocol.

*Warm Standby*: has a target foot print than a pilot light setup, and would most likely be running business critical applications in "standby".This type of configurtions could also be used as a test area for applications.

*Multi-Site Solution* Essentially clone your Prod environment which can be either on cloud on on-premise. Has an active-active configurations which means instacnes size and capacity are all running in full standby and can easily convert at the flip to a switch.
Methods like this could also be used to "load balance" using latency based routing or Route 53 failover in the event of an issue.

### Service Examples:

* ELB and ASG
* Amazon EC2 VM import connector
* Replicate from on-premise DB servers to RDS
* Automate the incresing of resources in the event of a disaster
* Use AWS import/export to copy large amounts of data to speed up replication times 
* Route 53 DNS Failover/Latency Based routing solutions
* Storage Gateway (Gateway-Cached volumes/Gateway Stored volumes)

