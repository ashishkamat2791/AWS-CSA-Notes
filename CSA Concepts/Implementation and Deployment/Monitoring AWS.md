# Monitoring your AWS environment:

## Use cloudwatch for:

* Shutting down inactive instances.
* Monitoring changes in your AWS environments with Cloudtrail configuration.
* Monitor instance resources and create alarms based off usage and availabilty:
    * EC2 instances have "basic" monitoring whch Clouwatch supports out of the box, and includes all metrics that can be monitored at the *hypervisor* level
    * Status checks which can autoamte recovery the of failed status checks by stopping starting the instance again.
    * EC2 metrics that include custom scripts to work with Cloudwatch:
        * Disk usage; Available Disk Space
        * Swap usage; Avaialbe Swap
        * Memory Usage; Available Memory

## Use Cloudtrail for

* Scuriry and Compliance
* Monitoring all actions taken against the AWS account.
* Monitoring (and being notified) of changes to IAM account (with CloudWatch/SNS Integration)
* Viewing what API keys/Users performed any given API action against an environment ( ie view user terminates a set of instances or an individual instance).
* Fulfilling auditing requirements inside of organizations.


## Use AWS Config for

* Receiving detailed configuration information about an AWS environment
* Taking a point in time "snapshot" pf all supported AWS resources to determine the state of your environment
* Viewing historical configurations within your environemnts by viewing the "snapshots".
* Receiving notifications whenever resources are created, modified, or deleted.
* Viewing relationships between resources, i.e, what EC2 instances an EBS volume is attached to.

 