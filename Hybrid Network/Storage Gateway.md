
# AWS Storage Gateway

* connects software appliances to cloud based storage such as Amazon S3.
* does this Storage Gateway virtual appliances, which conect directly to your local infrastructure as a file server, a local disk volume, or as a VTL
* can maintain frequntly accessed data on-premises (providing low-latency performance) while storing data in:
    * s3
    * EBS
    * Glacier
* Storage gateway also integrate your data with:
    * AWS encryption
    * IAM
    * Monitoring
## Gateway Cached Volume
* Create storage volumes and mount them as iSCSI devices on-premise servers.
* The gateway wil store the data to this volume in S3 and will cached frequntly accesed data on-premise in the storage devic.

## Gateway-Stored volumes
* Store all the data locally (on-premise) in storage volumes
* Gateway will periodically take snapshots of the data as incremental backups and store then on S3.
