# Other DB Services


## I] Dyanamo DB

![Alt_Text](https://images.g2crowd.com/uploads/product/image/social_landscape/social_landscape_1489711576/dynamodb.png "DynamoDB")
* Fast flexible NOSQL DB storage service for all application taht needs consitent,  singlr digit ms latency at any scale
* Fully managed DB & support both Document & Key-value Data Model
* Used for 
    * Gaming
    * Web Session
    * IoT
    * Web
    * Ad-Tech
* Stored on **SSD storage**
SSDs help us achieve our design goals of predictable low-latency response times for storing and accessing data at any scale. 
The high I/O performance of SSDs also enables us to serve high-scale request workloads cost efficiently, and to pass this efficiency 
along in low request pricing.
* Spread across 3 Geographically distinct data centres 



### Consisteny Models

**I] Eventual consistent Reads**

* Consisteny across all copies of data usually reached within seconds
* Repeating read after short period of time should return updated data.

**II] Strongly consistent reads**

* returns results that reflects all writes that received succesful response prior to read

```
Pricing is based on Capacity Units
Write is expensive than reads
```

### DynamoDB vs S3


Amazon DynamoDB stores structured data, indexed by primary key, and allows low latency read and write access to items ranging 
from 1 byte up to 400KB. Amazon S3 stores unstructured blobs and suited for storing large objects up to 5 TB. 
In order to optimize your costs across AWS services, large objects or infrequently accessed data sets should be stored in 
Amazon S3, while smaller data elements or file pointers (possibly to Amazon S3 objects) are best saved in Amazon DynamoDB.


### Limit

There is no limit to the number of attributes that an item can have. However, the total size of an item, including attribute 
names and attribute values, cannot exceed **400KB.**



## II] Redshift

![Alt_Text](https://clouda-assets.s3.amazonaws.com/upload/54d0e379d287c266052be6a0.png?1422975867"Redshift")
* Fast, powerful, fully managed, petabyte scale Data warehouse service
* Customer can go for small instance with just $0.5/hr with no commitments or upfront costs to petabyte or more for $ low price
per TB 1/10th of ocost
* use different types of architecture both from DB perspective & Infra layer
* OLAP



Configuration

**Single node with 160 GB**
* Multi Node 
  * Leader - manages client, send and recieive queries
* Compute
     * Store data & paerform queries & computations upto 128
 

 ### Columnar Data Storage

* Instead of storing data as a Series of rows, Redshift organizes data by colums
* columns base systems are ideal for data warehousing & analytics, where queirs often involve aggregate performed over large data sets.
* Since only columns involved in the queries are processed and columnar data is stored squentially on the storage media, 
 columnar-based syste,requires fewer I/Os greatly improving query performance

 ### Advanced compression

* Redshift employs multiple compresssion technique & often achieve significant compression relative to traditional 
 relative data storage
* doesnt require indexes or materilized views & uses less space than traditional RDBMS
* when loading data into empty table, Redshift automatically samples your data & select most appropriate compression algo



 **Massive Parallel Processing**


* automatically distributes data & query load across all nodes
* makes it easy to add nodes to Data warehouse & enbles you to mainain fast-query performance as DW grows

*****************
* Pricing is based on /unit/node/hr
* There is no charge for Leader Node, only compute node is charged


### Security


* In Transist- SSL
* At rest - AES 256
* Takes care Keys using cloud HSM


### Availabilty

* Only in 1 AZ
* can resotore snapshot to new AZ's in event of outage




## III]Elastic Cache

![Alt_Text](https://conceptdraw.com/a3134c3/p16/preview/640/pict--elasticache-aws-database---vector-stencils-library.png--diagram-flowchart-example.png "Elastc Cache")
* In Memory DB
* Improves performace of Web appliacations by allowing you to retrieve information from fast in-memeory caches, 
instead of Distributed DB
* Used to improve latency & throughput for many read-heavy appln workloads or compute intensive workloads
* improve app performance by stroring critical piece of data in memory for low latency acccess

### Types 
  * Memcached object caching system
  * Redis key-value store
  
## IV] Auroroa
 
 
 * mysql compatible relational DB 
 * 5 times better performace than mysql
 * 1/10 price of commercial DB
 * store with 10 GB increment to 64 TB (storage Autoscaling)
 * compute resource can schedule upto 32 vCPUs & 244 GB memory
 * 2 copies of data in each AZ, with min of 3 AZ 6 copies of data
 * designed to transparently hanlde loss of upto 2 copies of data without affecting DB write availabilty & 3 copies without affeciting
  read availabilty
 * Storage is self-healing Data blocks & disks continue scan for repairs automatically
  
  
