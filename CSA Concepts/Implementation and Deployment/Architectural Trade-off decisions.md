# Architectural Trade-off Decisions:

## Storage Trade-off Options

* S3 Standard Storage
    * 99.999999999 % durabilty and 99.99%, but the storage costs is cheaper.
* S3 RRS
    * durabilty is 99.99%, but cheaper storage cost.
    * Should be used for easily reproducible data, and you should take advantage of lost object notification usibg S3 events.
* Glacier
    * Requires abd extened timframe to check-n and check-out data from archiving.
    * Costs are significantly reduced compared to S3 storage options.

## Database Trade-off Option
 ### Running databases on EC2 instances:
 * have to manage the underlying OS.
 * have to build for high availability
 * have to apply your own backups.
 * Can use additional software to cluster MySQL
 * Requires more time to manage than RDS

 ### Manage RDS database provides:

 * Fully managed database updates and does not require managing of the underlying OS.
 * Provide automatic point-in-time backups.
 * Easily eanble Multi-AZ failover,and when a failover occurs the DNS is switched from the primary instance to the standby instnace.
 * If multi-AZ is enabled then backups are taken against the stand-by to reduce I/O freezes and updates are applied to standby then switched to the primary.
 * Easily create read replicas

 

