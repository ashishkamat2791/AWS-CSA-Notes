# DDos Mitigation

* When mitigating against DOS/DDOS attacks, use the same practice you would use on your on-premise componets:
* Firewalls
    * SG
    * NACL
    * Web application Firewall (WAF)
    * Host-based on Inline IDPS/IPS (Trend Micro)


* Along with your traditional approaches for DOS/DDOS attack mitigation, AWS provides capabilities based on its elasticity
    * You can potentially use Cloudfront to absorb DOS/DDOS flooding attacks.
    * A potential attackers trying to attack content behind Cloudfront distribution is likely to send most requests to Cloudfront distributions where the AWS infrastructure will absorb the extra requets with minimal to no impact on the back-end customer web servers.

* We MUST have permission to do Port Scanning on any of your EC2 instances.
* INGRESS Filtering on all incoming traffic onto their network
