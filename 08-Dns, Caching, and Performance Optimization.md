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