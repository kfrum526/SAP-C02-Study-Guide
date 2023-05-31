### Amazon EBS Deployement and Volume Types
    - Limited support for attaching multiple isntances
    - EBS volumes are replicated within an AZ
    - EC2 instances must be in the same AZ

### Amazon EBS Copying, Sharing and Encryption
    - EBS snapshots get saved in S3
    - Multiple snapshots of an instance are incremental
    - snpashots saved in a region, not AZ
    - Can create an AMI from the snapshot

## Copying and Sharing AMI's and Snapshots
    - Volume -> snapshot
        - Encryption state retained
        - same region
    - Snapshot -> Encrypted Snapshot
        - can be encrypted
        - can change regions
    - Unencrypted Snapshot -> Encrypted volume
        - Can be encrypted
        -Can change AZ
    - Uenncrypted Snapshot -> AMI
        - Cannot be encrypted
        - Can be shared with other accounts
        - can be shared publicly
    - Snapshot -> Snapshot
        - can change encryption key
        - can change regions
    - Encrypted Snapshot -> encrypted AMI
        - Can be shared with other accounts (custom key only)
        - cannot share publicly
    - Encrypted ami -> encrypted ami
        - can change encryption key
        - can change region
    - encrypted AMI -> EC2 instance
        - can change encryption key
        - can change AZ
    - unencrypted ami -> EC2 instance
        - can change encryption state
        - can change AZ
    - Encrypted Snapshot -> Encrypted Volume
        - can be encrypted
        - can change AZ

### Amazon S3 Encryptiong
    - Server-side encryption with S3 managed keys (SSE-S3)
        - s3 managed keys
        - unique object keys
        - master key
        - AES 256
    - Server-side encryption with AWS KMS managed keys (SSE-KMS)
        - KMS managed keys
        - Can be AWS managed keys
        - Or customer managed KMS keys
    - Server-side encryption with clinet provided keys (SSE-C)
        - client managed keys
        - not stored on AWS
    - Client-side encryption
        - client managed keys
        - not stored on AWS
        -Or you can use a KMS key
## Amazon S3 Default Encryption
    - All amazon s3 buckets have encryption configured by default
    - All new objects uploads to amazon s3 are automatically encrypted
    - There is no additional cost and no impact on performance
    - Objects are automatically encrypted by using server-side encryption with amazon s3 managed keys (SSE-s3)
    - To encrypt existing unencrypted Amazon S3 objects, you can use Amazon S3 Batch Operations
    - You can also encrypt existing objects by using the CopyObject API operation or the copy-object AWS CLI command
## Enforce Encryption with Bucket Policy
    - Enforce certain encryption with bucket policy

### AWS Storage Gateway

## File Gateway
    - The file system is mounted using NFS or SMB
    - A virtual gateway appliance runs on Hyper-V, VMware, or EC2
    - A local chache provides low latency access to recently used data
    - Files are stored as objects in S3
    - provides a virtual on-prem file server
    - Store and retrieve files as objects in Amazon S3
    - Use with on-prem applications, and EC2-based applications that need file storage in S3 for object-based workloads
    - File gateway offers SMB or NFS-based access to data in Amazon S3 with local chaching
## Volume gateway
    - cached volume mode
        - A chache of the most recent used data on-prem
        - entire data set is stored in s3
    - stored volume mode
        - Entire data set is stored on-prem
        - data backed up as point-in-time snapshots
        - entire dataset is stored on-site and is asynchronously backed up to S3 (EBS point-in-time snapshots). Snapshots are incremental and compressed
    - Suppo0rts block-based volumes only
    - Block storage -iSCSI protocol
## Tape Gateway
    - Backup server can use many common backup applications
    - S3 standard is used when writing tapes
    - once tapes are ejected from the backup app, they are stored in S3 glacier, Glacier deep archive or standard
    - used for backup with popular back up software
    - Each gateway is preconfigured with a media changer and tape drives. Suported by NetBackup, backup Exec, Veeam etc.
    - When creating virtual tapes, you select one of the following sized: 100GB, 200GB, 400GB, 800GB, 1.5TB, and 2.5TB
    - A tape gateway can have up to 1500 virtual tapes with a maximum aggregate capacity of 1PB
    - All data transferred between the gateway and AWS storage is encrypted using SSL
    - All data stored by tape gateway in S# is encrypted server-side with Amazon S3-managed Encryption Keys (SSE-S3)