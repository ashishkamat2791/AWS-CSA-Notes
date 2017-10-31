# Complex Access Controls

* IAM policies create extremly complex and granular permission policies for our users (all the way down to the resource level)
* IAM policies with resource level permissions:
    * EC2: Create permssions for instances such as reboot, start, stop, or terminate based all the way down to Instance ID
    * EBS volumes: Attach, Delete, Detach
    * EC2 actions that are not one of these above are not governed by resource-level at this time.
* This is not EC2 limited can also include services such as RDS, S3 etc.

* Addiotional security measures, such as MFA authentication are also available when acting on certain resources:
    Eg: You can require MFA before an API request to delete an object wtihin an S3 bucket.
    