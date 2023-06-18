### Amazon Route 53 Hosted Zones
    - A hosted zone represents a set of records belonging to a domain
    - You can migrate from another DNS provider and can import records
    - You can migrate a hosted zone to another AWS account
    - You can migrate from Route 53 to another Registrar
    - You can also associate a Route 53 hosted zone with a VPC in another account
        - authorize association with VPC in the 2nd account
        - Create an association in the 2nd account

### Route 53 Routing Policies
    - Simple
        - Simple DNS response providing the IP address associated with a name
    - Failover
        - If primary is down (based on health checks), routes to secondary destination
    - Geoloacation
        - uses geographic location you're in (e.g Europe) to route you to the closest region
    - Geoproximity
        - Routes you to the cloest region within a geographic area
    - Latency
        - Directs you based on the lowest latency route to resources
    - Multivalue answer
        - Returns several IP addresses and functions as a basic load balancer
    - Weighted
        - Uses relative weights assigned to resources to determine which to route to

### Route 53 Resolvers

## Outbound Endpoints
    - EC2 instance from inside a workload needs to use a on-prem DNS server
## Inbound Endpoint
    - A on-prem client needs to use Route 53 as a DNS resolver

### Amazon Cloudfront Origins and Distributions
    - Content is pushed fro morigin and cached in an edge location
    - Edge locations are distributed around the world
    - Users are directed to the nearest edge location by default

### Aamzon CloudFront Caching and Behaviors
    - Object is cached for TTL (defualt is 24 hours)
    - When the TTL expires the file is removed
    - Decreasing the TTL is best for dynamic contect, increasing the TTL is better for performance (and reduces load on origin
    
## Amazon CloudFront Caching
    - You can define a maximum TTL and a default TTL
    - TTL is defined at the behavior level
    - This can be used tor define different TTLs for different file types (e.g png vs jpg)
    - After expiration, CloudFront checks the origin for any new requests (Check the file is the latest version)
    - Headers can be used to control the cache:
        - Cache-control max-age=(seconds) - specify how long before CloudFront gets the object again from the origin server
        - expires - specify an expiration date and time
## ClouFront Path Patterns
    - The path pattern determines where to send the request
    - The default origin is used for any requests that don't match a path pattern
## Caching based on Request Headers
    - Yo ucan configure cloudfront to forward headers in the viewer request to the origin
    - CloudFront can then cache multiple version of an object based on the values in one or more request headers
    - Controlled in a behavior to do one of the following:
        - Forward all headers to your origin (objects are not cached)
        - Forward a whitelist of headers that you specify
        - Forward only the default headers (doesn't cache objects based on values in request headers)

### CloudFront Signed URLs and Origin Access Identity (OAI)

## CloudFront Signed URLs
    - Signed URLs provide control over access to content
    - Can specify beginning and expiration date and time, IP addresses/ranges of users
## CloudFron Signed Cookies
    - Similar to signed URL's
    - Use signed cookies when you don't want to change URLs
    - Can also be used when you want to provide access to Multiple restricted files (Signed URLs are for individual files)
## CLoudFront Origin Access Identity (OAI)
    - OAI has been replaced by OAC
## CloudFronty Origin Access Control (OAC)
    - Like a OAI but supports additional cases
    - AWS recommend the OAC for the following use cases:
        - ALl amazone s3 buckets in all AWS regions
        - Amazon S3 server-side encryption with AWS KMS (SS#-KMS)
        - Dynamic requests (PUT and DELETE) to amazon s3
    - Requires an S3 bucket policy that allows the CloudFront service principal

### CloudFront SSL/TLS and SNI

## CloudFront SSL/TLS
    - For CloudFront certificate must be issues in us-east-1 for ACM
    - Certificate can be ACM or a trusted third-party CA
    - Default CF domain name can be changed using CNAMES
    - S3 has it own certificate (can't be changed)
    - certificate can be ACM (ALB) or third party (EC2)
    - Origin certificates must be public certificates
## CloudFront Server Name Indication (SNI)
    - Multiple certificates share the same IP with SNI
    - request URL includes domain name which matches the certificate
    - Note: SNI works with browsers/clients released after 2010 - otherwise need dedicated IP

## Lambda@edge
    - Run Node.js and Python lambda functions to customize the content CloudFront delivers
    - Executes functions closer to the viewer
    - Can be run at the following points
        - After CloudFront receives a request from a viewer (viewer request)
        - Before CloudFront forwards the request to the origin (origin request)
        - After CloudFront recieves the response from the origin (origin respons)
        - Before CloudFront forwards the reponse to the viewer (viewer response)

### AWS Global Accelerator
    - User traffic ingresses using thje closest edge location
    - static anycase IP addresses to connect to multiple regions
    - Traffic traverse the AWS global network
    - Requests are routed to the optimal endpoint on failure nearest you