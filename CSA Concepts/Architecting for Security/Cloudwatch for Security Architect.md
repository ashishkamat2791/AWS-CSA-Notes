# Cloudwatch for Security Architect:

### Cloudwatch for Security:


* Requests are signed with an HMAC-SHA1 signature, calculated from the request and the user's private key.
* Cloudwatch control API is only accesible via an SSL encrypted endpoints.
* Cloudwatch access is given via IAM permission policies, essentially giving users permissins that are only needed (only give access to cloudwatch if they need access to Cloudwatch)
* Use Cloudwatch and Cloudtrail to monitor changes inside the AWS environment.
    * We can ask Cloudwatch to notify us (via SNS) if there has been changes, Eg;
        * Changes to IAM secuirty credentials
        * Assigning access policies to users.
        * Adding/deleting users
        
  **It is important to know how we can use Cloudwatch for security in our AWS Environment**
