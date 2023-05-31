### AWS Client VPN
    - VPN client connects over SSL/TLS (443)
    - VPN endpoint performs source NAT from CIDR to subnet associated to the VPN endpoint
    - Client VPN endpoints built for subnets
### AWS site-to-site VPN
    - AWS VPN is a managed IPSec VPN
    - A VGW is deployed on the AWS site
    - A customer gateway is deployed on the customer side
    - supports static routes or BGP peering/routing
    - private subnet RTB can point to the VGW
    - backup connection to direct connect
### AWS VPN CloudHub
    - A VGW is deployed on AWS site
    - Remote offices connect to the VGW in a hub and spoke model
    - Each office must use a uniquer BGP ASN
    - AWS site-to-site VPN to each office
    - Traffic may go between a VPC and a remote office
    - Network traffic between offices can be routed over the IPSec VPN
### AWS Direct Connect (DX)
    - Goes through an AWS Direct Connect location
        - AWS Cage
        - customer/aprtner cafe
        - a DX port (100-base-LX or 10GBASE-LR) must be allocated in a DX location
        * A cross between the AWS DX router and the customer/partner DX router
    - The customer router is connected to the DC router in the DC location
    - Time consuming to setup (weeks to months)
    - 1Gbps to 10Gbps
    * Benefits for DCx
        - Private connectivity between AWSand on-prem
        - Consistent network experience increated speed/latency and bandwidth/throughput
        - lower cost for large volumes of transfer data

    - A private VIF connects to a single VPC in the same AWS region using a VGW
    - A VIF is a virtual interface (802.1Q VLAN) and a BGP session
    - A public VIF can be used to connect to AWS public services in any region (but not the internet)
    
    *Multi-Vpc
        - Multiple private VIFs can be used to connect to multiple VPCs in the same region
        - VIFs can also be shared with other AWS accoutns - known as hosted VIFs
    
### Direct Connection (DX) ###
    - Speeds from 50Mbps to 500Mbps can also be accessed via an APN partner (uses hosted VIFs or hosted connections)
        - A hosted VIF is a single VIF that is shared with other customers
        - A hosted connection is a DX connection with a single VIF dedicated to you
    * DX connections are NOT encrypted~
    - uses an IPSec S2S VPN connection over a VIF to add encryption in transit
    - Link aggregation groups (LAGs) can be used to combine multiple physical connections into a single logical connection using LACP - provides improved spped

## DX-HA
    - DX locations are connected by redundant connections
    - Multiple DC locations exaist in metropolitan areas where AWS has regions
## DX + IPSec S3S VPN
    - The DX connection is the primary active path
    - An IPSec S2S VPN is the backup plan
    - Do not use if speed is over 2Gbps