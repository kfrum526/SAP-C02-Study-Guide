### Pricing options

# On-demand
    - Standard rate - no discount; no commitments; dev/test, short-term, or unpredicatable workloads
# Reserved
    - 1 or 3-year commitment; up to 75% discount; steady-state, predictable workloads and reserved capacity
# Spot Instances
    - Get discounts of up to 90% for unused capacity. Can be terminated at any time
# Dedicated Instances
    - Physical isolation at the host hardware level from instances belonging to other customers; pay per instance
# Dedicated Hosts
    - Physical server dedicated for use; socket/core visibility, host affinity; pay per host; workloads with server-bound software licenses
# Savings Plans
    - Commitment to a consistent amount of usage (EC2 + Fargate + Lambda); Pay by $/hour; 1 or 3-year commitment

## Amazon EC2 Billing
    - Per-second billing is for Amazon Linux and Ubuntu in On-Demand, Reserved, and Spot forms
    - Commercial Linux distros such as RHEL and SUSE ES use hourly pricing
    - EBS volumes billed per second; minimum of 1 minute

## Amazon EC2 Reserved Instances (RIs)
- Term is 1 or 3 years
- Can pay All upfront, Partial, Upfront, No Upfront
    - Standard RI
        - eChange AZ, instance size (Linux), networking type
        - use ModifyReservedInstances API
    - Convertiable RI
        - Change AZ, isntance size (Linux), networking type
        - Change family, OS, tenancy, payment options
        - use ExchangeReservedInstances API
    
## AWS Savings plans
    - Compute savings plan
        - 1 or 3-year; hourly commitment to useage of Fargate, Lmabda and EC2; any region, family, size, tenancy, and OS
    - EC2 Savings plan
        - 1 or 3-yea; hourly commitment to usage of EC@ within a selected region and instance family; any size, tenancy and OS

## Spot isntances
    - Spot instance
        - one or more EC2 isntances
    - Spot Fleet
        - launches and maintains the number of spot / on-demand instnaces to meet specified target capacity
    - EC2 fleet
        - launches and maintains specified number of Spot / On-Demand / Reserved Instances in a single API call
        - Can define separate OD/Spot capacity targets, bids, isntance types, and AZs
    - 2-minute warning if AWS need to reclaim capacity - available via instances metadata and cloudwatch events

## Dedicatged instances and Dedicated hosts

See slides in Images folder; Slide 198

### Amazon EC2 Pricing use cases

    - Developer working on a small project for several hours; cannot be interrupted
        - On-Demand
    - Computer-intensive, cost-sensitive distributed computing; can withstand interuption
        - Spot Instances
    - Steady-state, business critical, line-of-business application; continous demand
        - Reserved
    - reporting application, runs for 6 hours a day, 4 day a week
        - Scheduled reserved instance
    - Database with per-socket licensing
        - Dedicated host
    - Security-sensitive application, requires dedicated hardware; per-instance billin
        - Dedicated instances

### EC2 Placement Group Use Cases

    - Cluser
        - packs instances close together inside an AZ. This strategy enables workloads to achieve the low-latency network performance nexessary for tightly-coupled node-to-node communication that is typical of HPC applications
        - Uses enhances networking, low network latency and high throughput for inter-instance traffic
    - Partition
        - spreads your instances across logical partitions such that groups of instances in one partition do not share the underlying hardware with groups of instances in different partitions. This stategy is typically used by large distributed and replicated workloads, such as Hadoop, Cassandra, and Kafka
        - each partition is located on a separate AWS rack
        - Partitions can be in multiple AZ's (up to 7 per AZ)
    - Spread
        - Strictly places a small group of isntances across distinct underlying hardware to reduce correlated failures
        - each instance is located in a separate AWS rack

    - Tightly coupled application that requires low-latency, high throughput network traffic between isntances
        - Cluster
    - Distributed and replicated NoSQL database; requires separate hardware for node groups
        - Partition
    - small number of critical isntances that should be kept separate from each other
        - Spread

### Network Interface (ENI, EFA, ENA)

    - ENI
        - Basic adapter type for when yo7u don't have any high-performance requirements
        - Can use with all instacnes types
    - ENA
        - Enhanced networking performance
        - higher bandwidth and lower inter-instance latency
        - must choose supported instance type
    - EFA
        - Use with HPC and MPI and ML use cases
        - Tightly coupled applications
        - can use with all instance types

### Public, Private and EIP addresses

    - Pubic
        - Lost when the instance is stopped
        - used in public subnets
        - no charge
        - Associated with a private IP address on the isntance
        - cannot be moved between isntances
    - Private
        - Retained when the isntance is stopped
        - used in public and private subnets
    - EIP
        - Static public IP address
        - you are charged if not used
        - associated with a private ip address on the instances
        - can be moved between instances and ENA

### Advanced Autoscaling

## Target Tracking
    - ASGAverageCPUUtilization
        - Average CPU utilization of the ASG
    - ASGAverageNetworkIn
        - Average number of bytes received on all network interfaces by the AFS
    - ASGAverageNetworkOut
        - Average number of bytes sent out on all network interfaces by the ASG
    - ALBRequestCountPerTarget
        - Number of requests completed per target in an ALB target group
## Target Tracking with SQS
    - scale based on number of message in queue
## Simple scaling
    - CPU=70%, alarm set to >= 60%, launch 2 instances, wait 300 seconds before allowing another scaling activity
## Step scaling
    - Alarm set to >= 60%, CPU = 70%, launch 2 instances
    - Alarm set to >= 60%, CPU = 80%, launch 4 instances
## Schedule Scaling
    - Schedule set to scale at X:XX AM/PM, launch X instances
        - desired count
        - minimum instances
        - maximum instances
        - Recurrence
        - Start time
## Scaling process
    - Launch
        - Adds a new EC2 instance to an ASG
    - Terminate 
        - Removes an EC2 isntance from the group
    - AddToLoadBalancer
        - Adds instances to an attached ELB or TG
    - AlarmNotification
        - Accepts notifications from CloudWatch alarms that are associated with the group's scaling policies 
    - AZRebalance
        - Balances the number of EC2 isntnaces in the group evenly across all of the sepecified AZ's
    - HealthCheck
        - Check the health of the instances and marks an instance as unhealthy if Amazon EC2 or ELB tells Amazon EC2 auto scaling that the instance in unhealthy
    - ReplaceUnhealthy
        - Terminates instances that are marked as unhealthy and then creates new instances to replace them
    - ScheduleActions
        - Performs scheduled scaling actions
## Additional Scaling Settings
    - Cooldowns
        - used with simple scaling policy to prevent Auto Scaling from launching or terminating before effects of previous activities are visible. Defaultg value is 300 seconds (5 minutes)
    - Termination policy
        - Controls which instances to trerminate first when a scale-in event occurs
    - Termination protection
        - Prevents auto scaling from terminating protected instances
    - Standby State
        - Used to put an inst ances in the InSerivce state into the Standby state, update or troubleshoot the instance
    - Lifecycle hook
        - Used to perform custom actions by pausing inst ances as the ASG launched or terminates them

### Types of Elastic Load Balancer (ELB)

## Application Load Balancer
    - Operates at the request level
    - Routes based on the content of the request (Layer 7)
    - Suports path-based routing, host-based routing, query string parameter-based routing, and source IP address-based routing
    - Supports isntances, IP addresses, Lambda functions and containers as targets
    - Cannot have EIP
## Network Load Balancer
    - Operates at the connection level
    - routes connections based on IP protocol data (Layer 4)
    - Offeres ultra high performance, low latency and TLS offloading at scale
    - can have static IP/Elastic IP
    - Supports UDP and static IP addresses as targets
## Gateway Load Balancer *not yet on the test
    - Used in front of virtual applicances such as firewalls, IDS/IPS, and deep packet inspection systems
    - Operates at Layer 3 - listens for all packets on all ports
    - Forwards traffic to the TG specified in the listener rules
    - Exchanges traffic with appliances useing the GENEVE protocol on port 6081

### Routing with ALB and NLB

## Application Load Balancer (ALB)
    - Target groups are used to route requests to registered targets
    - A rule is configured on the listener - ALB's listen on HTTP/S
    - Requests can be routed based on the path in the URL
    - Path-based routing and Host-based routing
## Network Load Balancier (NLB)
    - NLB nodes can have elastic IPs in each subnet
    - NLB'd listen on TCP, TLS, UDP OR TCP_UDP
    - A seperate listener on a unique port is required for routing
    - targets can be EC2 instances or IP addresses
    - Targets can be outside a VPC

### ALB and NLB Access Control and SSL/TLS
    - No secuity group for NLB, only on the EC2
    - ALB has security groups
    - CLB and ALB use private IP of their ENI's as source address
    - Client (IP=A), NLB (IP=B), instance specified by the insstance ID on the NLB, the source IP will be IP=A (client)
    - Client (IP=A), NLB (IP=B), instance specified by the IP Address on the NLB, the source IP will be IP=bn (NLB)
        - Applicable to TCP and TLS - for UDP and TCP_UDP should be IP=A
    - When using an NLB with a VPC endpoint or AWS GA source IPs are private IP's of NLB Nodes

## SSL/TLS Termination
    - ALB
        - ACM certificate or certificate imported into ACm or IAM
        - With a L7 ELB a new connection is established with the isntance
        - Self signed cert can be use for encrytion from ALB to instance
    - NLB
        - Public certificate must be used  (encryption straight through)
        - single encrypted connection
        - SSL/TLS cert on NLB and SSL/TLS cert on instance (2 seperate encrypted paths)

## Session state and sessions stickiness

## Storing sessions state
    - sessions data such as suthentication details stored in DynamoDB Table
    - Sessions data retrieved from dynamoDB table
    - user does not need to re-authenticate
    - elasticache is also a popular solution for storing session-state data
## Stick sessions
    - Cookie is generated and client bound to instance for cookie lifetime
    - Session data such as authentication details stored locally
    - client is directed to another isntance on failure
    - if an instance fails, session state is lost - use with sesssions state store for more resiliency

### AWS Batch
    - batch job
        - A job is a unit of work such as a shell script, executable, or docker container images
    - a job is submittedf to a queue until scheduled onto a compute environment
    - batch launches, manages, and terminates as required (EC2 and ECS/Fargate)
    - managed or unmanaged resources used to run the job

### AWS Lightsail
    - Power virtual servers built for reliability and performance
    - 1 month free trial, starting at 3.50/month (Linux), $8/month (windows)
    - low cost and ideal for users with less techincal expertise
    - computer, storage and network
    - preconfigured virtual servers
    - viirtual servers, databases and load balancers
    - SSH and RDP access
    - can access amazon VPC
    - EXAM TIP: typically comes up in use cases where an easy method of deploying a virtual server is required by a ruser with little or no AWS expertise

### Architecture patterns - compute
    - Requirement: HA and elastic scalability for web servers
        - Solution: Use amazon EC2 AS and an ALB across multiple AZs
    - Requirement: Low-Latency connections over UDP to a pool of inst ances running a gaming application
        - Solution: Use a NLB with a UDP listener
    - Requirement: Clients need to whitelist static IP addresses for a HA load balanced application in an AWS region
        - Solution: Use an NLB and create static IP addresses in each AZ
    - Requirement: Application on EC2 in an ASG requires disaster recovery across region
        - Solution: Create an ASG in a second region with the capacity set to 0. Take snapshots and copy them across regions (Lambda or DLM)
    - Requirement: Application on EC2 must scale in larger increments if a big increase in traffic occurs, compared to small increases in traffic
        - Solution: Use AS with a step scaling policy and configure larger capacity increase
    - Requirement: Need to scale EC2 instances behind an ALB on the number of requests completed by each inst ance
        - Solution: Configure a target tracking policy using the ALBRequestCountPerTarget metric
    - Requirement: Need to run a large batch computing job at the lowest cost. Must be managed. NOdes can pick up where other left off in case of interuption
        - Solution: Use a managed AWS Batch job and use EC2 spot inst ances
    - Requirement: A tightly coupled HPC workload requries low-latency between nodes and optimum network performance
        - Solution: Launch EC2 instances in a single AZ in a cluster placement group and use an EFA
        - EXAM TIP: HPC usually will be followed by EFA
    - Requirement: LOB application recieves weekly burst of traffic and must scale for short periods - need the most cost effective solution
        - Solution: use reserved instances for minimum required workload and then use spot instances for the bursts in traffic
    - Requirement: Application must startup quickly when launched by ASG but requires app dependencies and code to be installed
        - Solution: Create an AMI that includes the application dependencies and code
    - Requirement: Application runs on EC23 behind an ALB. Once authenticated users should not need to breauthenticate if an instance fails
        - Solution: Enable sticky sessions for the TG or alternatively use a sessions store such as DynamoDB