# Direct Connect

* Service that provides a dedicated network connection between your network and one of the AWS Direct Connect locations.
* This is done through an authorized Direct Connrct Provider (Eg: VeriCzon)

* Does not require hosting any router/hardware at the Direct Connect Provider location ,only requires a Direct Connect location and a participating bakup provider.
* An AWS Direct Connect location provides access to the region It is associated with
* It does not provide access to other AWS regions.

## Direct Connect Benefits

* **Reduced network costs:**
    * Reduce bandwidth commitment to corporate ISP over public Internet.
    * Data transferred over direct connect is billed at a lower rate by Amazon (data in/out)

* **Increase Network consistency**
    * Dedicated private connections reduce latency (over sending the traffic via public routing)

* **Dedicated private network connection on premise:**
    * Connect the direct connect connection to VGW in your VPC for  a dedicated private connection from on-premise to VPC.
    * Use Multiple VIF (Visual Interface) to connnect to multiple VPcs

## Cross network Connection (Cross Connect):
The **physical connection between your network and the Direct Connect authorized partner**, which then handles the routes and connection to AWS networks.


## Public Virtual Interfaces:

* allows you use a  Direct connect to connect public AWS endpoints:
    * Any AWS serice (Eg DyanamoDB, S3)
* Requires public CIDR block range
* And even though we are accesing public endpoints, the connection maintain consistent traffic consistency as it is sent over your dedicated network.

## Private Virtual Interface

* allows you to interface with AWS VPC
    * with automativ rules discovery using BGP
    * Requirs public or private ASN no
* Can only communicate with Internet with internal IP addresses inside of EC2.
* Cannot access public IP addresses, as Direct connect is NOT an Internt provider
* This is a dedicated private connection which is like a VPN.
For best-practices, use 2 Direct Connect connections for active=active or active-failover availability.
* You can also use VPN as a backup to direct connectios.
* You can create multiple private virtual Interfaces to multiple VPC's at the same time.

