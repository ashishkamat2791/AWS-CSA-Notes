# How to Design Cloud Services & Best practices?

* *Design for failure* and create self-healing application environments.
* Always design application with instances *in atleast two availability zones*
* Gurantee that you have "reserved" capacity in the event of an emergeny purchasing reserved instances in a designated recovery availabilty zone (AWS does not gurantee on-demand instance capacity).
* Rigorously test to find singlr point of failure and apply high availabilty.
* Always eanble RDS multi-AZ and automated backups (InnoDB tablr support only for MYSQL)
* Utilize Elastic IP address for fail-over to stand-by instances when auto-scaling and load-balancing are not avaialble
* Use Route 53 to implement DNS failover technique that include:
    * Latency based routing
    * Failover DNS routing
* Have a disaster recovery and backups strategy that utilizes:
    * Multiple regions
    * Maintain upto date AMI's (and copy from one region to another)
    * Copy EBS snapshots to other regions (use CRON jobs that takes snapshots of EBS)
    * Automate everything in order to easily re-deploy resources in the event of a disaster
    * utilize bootstraping to quickly bring up new instances with minimal configuration and allows for generic AMI

    * Decouple app components using SQS (when availble)
    * "Throw away" old or broken instances.
    * Utilize cloudwatch to monitor infrastructure changes and health.
    * Utilize multipart uploadfor S3 uploads (for object over 100MB)
    * Cache static content on Amazon cloudfront using EC2 or S3 origins

    * Protect your data in transist by using HTTPS/SSL endpoints
    * Protect data at rest using encrypted file systems or EBS/S3 encryption options.
    * Connect to instances inside of the VPC using Bastion host or VPN connection.
    * Use IAM roles on EC2 instances instead of using API keys *Never store API keys on AMI*
    
