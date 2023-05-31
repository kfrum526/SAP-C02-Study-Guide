### Advanced VPC

## AWS Outposts
    - use cases:
        - Use aws services on prem
        - Use AWS API's on prem
## AWS Wavelength zones
    - use cases:
        - Single-digit ms latency to mobile devices/users
        - live videos, ML, AR/VR
## AWS Local zones
    - Attached to IGW or VGW to control incoming traffic

## Nat instance
    - created in public subnet
    - EIP and private IP
    - managed by you
    - scale up and enhanced net
    - No HA unless multiple NATs
    - Need to assign Security Group
    - Can use as bastion
    - Can implement port forwarding
## Nat gateway
    - Managed by AWS
    - Elastic scales up to 45Gbps
    - provides HA within AZ and can be placed in Multi-AZ
    - No security groups
    - can't access through SSH
    - Choose EIP at creation
    - Does not support port forwarding

## VPC peering
    - doesn't support transitive
    - CIDR's can't overlap
    - Can be between regions and/or accounts
# VPC Endpoints
    - Inerface endpoint:
        - creates endpoint eni
        - each interface endpoint can connect to one of many AWS services
        - or can connect to amazon privatelink powered service
        - connects EC2 instances connects to public AWS service using private IP's
# Gateway Endpoints
    - uses rtb entry
    - EC2 connects privately
    - IAM policies can be applied
    - Bucket policies can limit endpoint

## Interface
    - ENI with Private IP
    - Uses DNS to redirect traffic
    - API gateway, CloudFormation, etc
    - Security groups
## Gateway
    - Target to a specific route
    - uses prefix lists in the table to redirect traqffic
    - S3, and DynamoDB
    - Endpoint policies
    