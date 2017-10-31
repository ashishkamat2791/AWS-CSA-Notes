 # Encryption Solutions:

  ### S3 has built-in features that allow you to encrypt your data:
    * AES-256 bit encryption that encrypt data-at-rest in an S3 bucket.
    * AWS will decrypt the data and send to you when you download it.

### EBS encryped solutions:
* You can select to have all data encrypted that is stored on an EBS for volume
* If a snap-shot it taken, that snapshot automatically encrypted

### RDS Encryption:
* Aurora, MySQL,Oracle, PostgreSQL, and MS SQL all support in this feature.
* Encrypts the underlying storage space for the instance.
* Automated Backups are encrypted (as well as snapshotd)
* RDS provides SSL endpoints to encrypt a connection to DB instance.
