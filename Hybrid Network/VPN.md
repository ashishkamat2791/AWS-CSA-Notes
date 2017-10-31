# Virtual Private Netwok

* A virtual private network enables the ability to extend a subnet from one geographic location to another location on two separate networks
* Extending the subnets allows network at location "A" to communicate internally with all resources at location "B"
* This is essentially "extending" the on-premise network to the cloud, or the cloud to the on-premise network


* **For AWS**, this allows to communicate with all resources (like an EC2 instance) internally without the need for public IP addresses and an internet gateway.
* It also provides an additional level of security by ensuring that traffic sent using the VPN is encrypted


* The VPN connection has two parallel routes (IPSec tunnels), which is for redundancy.
* Only one Virtual Private Gateway can be attached to a VPC (just like one IGW can be attached to VPC)
* A VPC can have both VPG and IGW attached at the same time.

## VPN Connection

* The VPN connection is the actual link between VPG and Customer Gateway.
* This connection is setup and managed in AWS.
* Each connection uses 2 IPSec tunnels for redundancy.

## Customer Gateways

* A **Customer Gateway** is a physical device or software application at the on-premise location that acts as the "connector" to VPN connection.
* In your AWS account, the **Customer Gateway** is where you configure the public IP (internet routable static IP) address of the physical device or software application at the on-premise location

**Both a VPG and Customer Gateway are required to establish a VPN connection**

## VPG:

* A **Virtual Private Gateway** acts as the "connector" onthe VPC (AWS) side of the VPN 
* VPG is connected to VPC

**Both VPG and Customer Gateway are required to establish VPN connection**

## Router
* AWS has dsipensed with the concept of ahving users physically setup and manage a "router".
* However, It is important understand that route tables are actually part of "router" assigned to your VPC
* When setting up a VPN, the **route table** (for the subnet you wish to extend) must include routes for on-premise network that are used by the VPN. and point to the VPG.
