# ELB
 
* Internet facing load balancer has a publicly resolvable DNS name.

* Domain names for each content on the EC2 instances served by the EB , is resolved by the Internet DNS servers to the ELB DNS names ( and hence IP adresse)
* This is how traffic from Internet is redirected towards instances via load balancers


## ELB Listeners

* Process to check for connection requests
* You can configure protocol/port on whic your EL listener listens for connection rerqusts
* Frontend listeners check for traffic form cliensts to the ELB
* Backend listeners are configured with protocol/port to check for traffic from ELB to the EC2 instances

* It may take soemtime for the registation of EC2 instances under the ELB to complete.
* Registered EC2 instances are those that are defined under the ELB
* ELB has "nothing" to do with outbound traffic that is initiated/generated from the registered EC2 instances destined to the internet, or to any other instances within the VPC.
* ELB only has to do with inbound traffic destined to the EC2 registered instances (as the destination),
and the respective return traffic.
* **You start to be charged hourly once your ELB is active**
* If you do not want to be charged or you do not need the ELb anymore, you can delete it.
* Before  you delete the ELB, It is recommended that you point the Route53 to somewhere else other than ELB
* Deleting ELB does not affect, or delete EC2 instances registered with it.
* ELB forwards traffic to eth0 to your registered instances
* In case the EC2 instances has multiple IP addresses on eth0, ELB will route the traffic to its primary IP address.

* Front End listeners Client to ELB
* Backend From ELB to EC2 instances
* You can confgure multiple listensres with different protocols/ports both on Front End and backend



## ELB Scope

### Addding Tags
* ELB supports **IPV4** only.
* To ensure that rhe ELB service can scale ELB nodes in each AZ ensure that the subnet defined to the load balancer is atleast /27, and at least 8 available IPs to the ELB nodes to scale

* ELB uses this IP addresses to Open/connect with your registered EC2 instances

### Health Check

* For fault toleance It is recommended that you disrtibute your registered EC2 instances across multiple AZ within VPC region

* Ideally, have the same no of registered instsnces in each AZ is possible 
* The load balancers also monitors the health of its registered instances and ensures that it routes traffic only to healty instances

* A healthy instsnce shows as "In Service" under the ELB
* When the ELB detects an unhealthy instacne it stops routing traffic to that instance 
* An un-healthy instance shows as "Out of Service" under the ELB

* When the ELB service detects the EC2 instance is back healthy, It resumes traffic back to that


### By default 

* AWS console uses ping HTTP (port 80) for health checks
* API uses ping TCP (port 80) for health checks
* Registered instances must respond with 200 status code witihin timout period, else, IT will considered as unhealthy
* Response timeout is 5 seconds (rsnge 2-60 seconds)


#### Health Check Interval:
* Period of time between health check
* Default 30(range 5-300 sec)


####Unhealth Threshold
* No of conseccutive failed health checks that should occur before the instance is decided unhealthy
Range 2-10
* Default 2

#### Healthy Threshold
* No of consecutive succesful health checks that must occur before the instance is considered as healthy
Rane 2-10
* Default 10

#### Healath check Interval:
* Period of time between health checks
* Default 30 (range 5-300 sec)



## Cross Zone Load balancing

* disabled by default

* By defalutt, distribute traffic evenly between the AZs, the AZs it is defined in, without consideration to the no of registered instances in each AZ.


## ELB a service

* can be cofigured through AWS CLI, SDKs Query APIs
* names you choose must be unique within the account E//lBs in the AWS region

* ELB is **region** specific, so all registerd EC2 instances must be within same region but can be a different AZs (use Route 53 to load balance in different regions)
* The names can be upto 32alphanumeric characters and can NOT start or end with hyphen (-)

* To define ELB in AZ you can select one subnet in that AZ
* Only one subnet can be defined for the ELB in an AZ
* If you try and select another one in the same AZ it will replace the former one

* If you registered instances in a nAZ but do not defined a subnet in that AZ for ELB,
The instancs will not receive traffic from ELB
* The ELB is most effective if there is one registerred instance at least in each AZ


## ELB positioning

* Internet facinga
* Internal facing

* **1) Internet facing**
* ELB nodes will have public IP addesses,
* DNS will resolve the ELB DNS name to these IP addresses
* It routes traffic to the private IP addresses to your registered EC2 instances,
You need one "Public" subnet in each AZ where the internet facing ELB will be defined, such that the ELB will be able to route internet traffic
* Define this in ELB configuration

* **2) Internal  facing**
* ELB nodes will have private  IP addesses,
* It routes traffic to the private IP addresses to your registered EC2 instances,

#### Name format

* Public facing: name-2122324.region.elb.amazonaws.com
* Intranet facing: internal-name-2122324.region.elb.amazonaws.com

### ELB and secuirty Groups


* Defult VPC AWS will automatically create one for ELB with all required rules/ports
* Non-default, you can choose SG for ELB from exiting If not Deafut SG of VPC is assigned
* You must assign that
This will control traffic that can rach your ELB's front end listeners
* It must allows health check protocol/ports & listeners protocol/port  (actual traffic) to reach your registered EC2 instances in the backend
* You must also ensures hat the subnet's NACL allow traffic to/from the ELB both ways


#### Security settings

* Internet facing -- Source 0.0.0.0/0 Protocol: TCP Port: ELB Listener 
* Internal ELB  -- Source: VPC CIDR Protocol: TCP Port: ELB Listener


### Listeners

**Layer 4 TCP/SSL**

* When TCP listeners are used for Front-End and Back-End connections, the ELB forwards requests to the EC2 registered, back-end instances without modifying the headers
* When the ELB receives the request, it tries to open TCP connection to the EC2, back-end, instances on the port specified in the listeners configuration
* Because of this interception, EC2 instance logs would show ELB IP address as the source IP at the EC2 instance reciived packets.

* Enable proxy protocol on the ELB to force the ELB to carry the connection request details with the request sent to EC2 instace
To Enable this:
-- Ensure request fro Client to ELB does not pass through a proxy server with proxy prtocol enabled
This will cause the backend instance to receive the requests with 2 proxy headers.


* Confirm that your EC2 instances can porces proxy/protocol information


**Layer 7 Application HTTP/HTTPS** 

* To use HTTPS listener, the ELB must have a X.509 SSL/TLS server certificate, which will be used to terminate the Client to ELB HTTPS connection
* Using this certificate the ELB will terminate then decrypt the Client session on the ELBitself before sending the request to Backened EC2 instances known as SSL termination
* When using HTTP/s for Fron end listeners, the ELb terminates the seesion,carries the heraders, in request, and sends the request to the EC2, back end, instances.

You can use HTTP-X-Forwarded-For headers for the request sent from the ELB to the backend instances (EC2 instances APPs need the X-Forward-for header)

## Sticky Session (Session Affinity)

* Whereby the ELB binds a client/user session/requests to a specific backend EC2 instance
* Not fault Tolerant
* requires SSL termination on the ELB, require X.509 certificate configured on the ELB
* It must be in the same region

#### Duration determined by:
* the applicatio inserting session cookies,
* If application does not have its own cookies ELB can be configured to create one determines stickiness duration
* The ELB inserts a cookie in the response to bind subsequent requeststo same backend instances

### When using application cookie
* If cookie expires or remove, the seesion is no longer a sticky session and ELB uses the normal, route to least loaded backend instance, untill a new cookie is inserted

