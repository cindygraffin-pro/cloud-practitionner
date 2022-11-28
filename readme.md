# AWS Cloud Practitioner

Cloud Practitioner exam - CLF-C01

## Cloud Computing

**How the web works ?**

The client will use the network to route the packets, the data into the server, then the server will reply to us and we will get the response.  
Client and server have an IP address that allow each one to reach other.

**What is a server composed of ?**
- CPU: little piece that do some computations, it do some calculations and find results
- RAM: Fast memory, allow to store and fin information fastly
CPU + RAM = like a brain
- Storage Data (for ex files)
- Database: store data in a structured way
- Network: cables, routers and servers connected with each other (routers, switch, DNS server)

Router = networking device that forwards data packets between computer networks  
Switch = takes a packet and send it to the correct server/client on the network

**What is Cloud Computing ?** 
- on-demand delivery of compute power, database storage, apps and others IT resources -> on demand self-service
- through a cloud services platform with pay-as-you-go pricing
- provision exactly right type and size of computing resources needed
- access as many resources almost instantly -> broad network access
- simply way to access servers, storage, db and a set of app services
- multi-tenancy and resource pooling: multiple customers can share the same infra and app with security and privacy
- rapid elasticity and scalability

**Deployment Models of the Cloud:**
- Private Cloud: Cloud services used by a single organization, not exposed to the public, complete control, security
- Public Cloud: Cloud resources owned and operated by a third-party cloud service provider delivered over the Internet
- Hybrid Cloud: keep some servers on premises and extend some capabilities to the Cloud, control over sensitive assets

**Six advantages:**
- Trade capital expense (CAPEX) for operational expense (OPEX)/variable expense: pay on demand, reduce total cost of ownership (TCO) & Operational Expense (OPEX)
- benefit from massive economies of scale
- stop guessing capacity
- increase speed and agility
- stop spending money running and maintaining data centers
- go global in minutes: leverage the AWS global infra  
-> flexibility,  cost-effectiveness, scalability, elasticity, high availability and fault tolerance, agility

**Types of Cloud Computing:**
- IasS: provide building blocks for cloud IT, provides networking, computers and data storage, flexibility (EC2, google cloud, azure ...)
- PaaS: removes the need for the organization to manage the underlying infra, focus on deployment and management of the infra (heroku ...)
- SaaS: complete product that is run and managed by the service provider (gmail, dropbox ...)

**Pricing:**
- Pay for compute time
- pay for data stored in
- pay for data transfer out but not in

**AWS Global Infra:**
- AWS Regions: all around the world (eu-west-3 for ex) -> a region is a cluster of data centers, most services are region-scoped  
*How to choose an AWS Region ?*
  - Compliance with data governance and legal requirements: data never leaves a region without explicit permission
  - Proximity to customers: reduced latency
  - Available services within a Region
  - Pricing: varies region to region
- AWS Availabality Zones: 
  - usually 3, min is 2 and max is 6 (for ex ap-southest-2a, ap-southest-2b)
  - Separate from each other, discrete data centers with redundant power, networking and connectivity. 
  - They are connected with high bandwidth and ultra-low latency. 
  - Link together, they will form a region. 
  - One or more data centers in the same location
  - all traffic between AZ is encrypted
- AWS Data Centers
- AWS Edge Locations / Points of Presence: 216 points of presence in 84 cities across 42 countries, content is delivered to end users with low latency. 

**Shared Responsability:**
- Customer: responsability for the security *in* the cloud
- AWS: responsability for the security *off* the cloud

**AWS Acceptable Use Policy:**
- no illegal, harmful, or offensive use or content
- no security violations
- no network abuse
- no e-mail or other message abuse

**AWS Resource Groups:**
Helps organizing AWS resources, manage and automate tasks on large numbers of resources at a time.

## IAM

Identity and access management, Global service

**CLI:**

`aws iam list-users`: list all the users in the account

**Permissions:**
- Users or Group can be assigned JSON documents called policies, that define permissions of those users
- Apply the least privilege principle

Online policy is a policy attach to only one user. For users in group, they inherit the same policy. An user that belongs to two groups or more will inherit policy of each group.

**Policy Structure:**
- JSON document
- Version number
- id to identify the policy (optional)
- statement: (req)
  - sid: an identifier for the statement (opt)
  - effect: whether the statement *Allow* or *Deny* access
  - principal: account/user/role to which this policy applies to
  - action: list of actions this policy allows or denies
  - resource: list of resources to which the actions applied to
  - condition: when this policy is in effect (opt)

**Password Policy:**
- strong passwords
- options:
  - min pw length
  - require specific character type
  - all all IAM to change their own password, or to change after some time (pw expiration)
  - prevent pw re-use

**MFA:**
- multi factor authentication
- password we know + security device owned  
-> if pw is stolen or hacked, account is not compromised
- different options: 
  - virtual MFA device like Google Authenticator (one phone) or Authy (multi device), they support multiple tokens on a single device
  - Universal 2nd factor (U2F) Security Key: physical device like YubiKey (3rd party), support multiple root and IAM users, plug into USB port, open auth standard hosted by the FIDO alliance
  - Hardware Key Fob MFA Device: generates a six-digit numeric code based upon a time-synchornized one-time pw algo
  - Hardware Key Fob MFA Device for AWS GovCloud (US)

**IAM Roles for Services:**
- some AWS services will need to perform actions on our behalf
- we'll assign permissions to AWS services with IAM roles
- for ex, EC2 Instance Roles, Lambda Function Roles, etc...
- Just one IAM role to a single instance

**Security Tools:**
- IAM Credentials Report (account-level): a report that lists all our account's users and the status of their various credentials
- IAM Access Advisor (user-level):  shows the service permissions granted to a user and when those services where last accessed, it can be use to revise policies

**IAM Access Analyzer:**
- helps identify the resources in org and accounts, such as S3 buckets or IAM roles, shared with an external entity
- let us identify unintended access to our resources and data

**Shared Responsability Model for IAM:**
- AWS responsibilities:
  - Infrastructure (global network security)
  - config and vulnerability of services they offer
  - compliance validation
- User:
  - Users, groups, policies management and monitoring
  - Enable MFA on all accounts
  - rotate all keys often
  - use IAM tools to apply appropriate permissions
  - analyze access patterns & review permissions


## AWS SDK

AWS Software Development Kit:
- language specific APIs
- enables to access and manage AWS services programmatically

## AWS CLI

`aws configure`: configure account on CLI with access keys

**Access keys:**
- use for programmatic access to AWS resources from the WS CLI/API
- long-term credentials for an IAM user or the AWS account root user

## EC2 

Elastic Compute Cloud = way of doing IaaS  

- Renting virtual machines (EC2)
- Storing data on virtual drives (EBS)
- Distributing load across machines (ELB)
- Scaling services using an auto-scaling group (ASG)

**Sizing and config options:**
- Different OS: Linux, Windows, or MacOS
- CPU: compute power & cores
- RAM
- Storage space:
  - network-attached (EBS & EFS)
  - hardware (EC2 Instance Store)
- Network card: speed of the card, public IP address
- Firewell rules
- Bootstrap script: EC2 User Data

**EC2 User Data:**
- bootstrapping = launching commands when a machine starts
- run once at first start
- automate boot with tasks such as installing updates, software, dowloading files from the internet, etc..
- the script runs with the root user

:warning: If we stop and relaunch an instance, its PUBLIC Ip addresses can change 

**Instance Types:**

- General Purpose:
  - balance between compute, memory and networking
  - diversity of workloads such as web servers or code repo
- Compute Optimized:
  - great for compute-intensive tasks that require high perf processors
  - for ex batch processing workloads, media transcoding, high perf web servers/computing (HPC), gaming servers, machine learning, etc..
- Memory Optimized:
  - fast perf for workloads that process large data sets in memory
  - for ex relational/non-relational db, distributed web scale search stores, in-memory db optimized for business intelligence (BI)
  - app performing real-time processing of big unstructured data
- Storage Optimized:
  - storage-intensive tasks that require high, sequential read and write access to large data sets on local storage
  - for ex online transaction processing (OLTP) systems, relationnal and NoSQL db, cache for in-memory db, data warehousing app, distributed file systems
  
Common pattern, for ex **m5.2xlarge**:
- m: instance class
- 5: generation of the hardware
- 2xlarge: size within the instance class

**Security Groups:**
- Control how traffic is allowed into or out of our EC2 Instances.
- only contain *allow* rules
- rules can reference by IP or by security group
- act like a "firewell" on EC2 instances
- They regulate access to ports, authorised IP ranges, control inboud and outboud network
- can be attached to multiple instances
- locked down to a region/VPC (virtual private cloud) combination
- live "outside" the EC2
- it's good to maintain one separate security group for ssh access
- *connection refused* will come from an app error or not launched
- by default, all inboud traffic is blocked and all outbound is authorised

**Ports:**
- 22: SSH - log into a Linux instance
- 21: FTP - upload files into a file share
- 22: SFTP - upload files using SSH
- 80: HTTP - access unsecured websites
- 443: HTTPS - access secured websites
- 3389: RDP (Remote Desktop Protocol) - log into a Windows instance

**SSH:**
- CLI utility for Mac, Linux and Windows >= 10
- Also have Putty for all Windows
- And EC2 Instance Connect thzt will use the web browser and is valid for all
- allow to control a remote machine using the cli

`ssh -i file.pem ec2-user@35.180.34.141`: connect to an ec2 instance via ssh, ec2-user is the name of the user and then the public IP address  
`chmod 0400 file.pem`: give the right to read on the pem file

**Pricing:**
- On-demand instance: short workloads, biling per second for Linux and Windows, and per hour for others
- reserved (1 & 3 years): 
  - Reserved Instances: long workloads, reserved instance's scope (regional or zonal)
  - Convertible Reserved Instances: long workloads with flexible instances, allow to change instance type, family, OS, scope and tenancy
- Saving Plans (1 & 3 years): commitment to an amount of usage, long workloads, specific instance family & AWS region but flexible with size, OS and Tenancy (Host, Dedicated or Default)
- Spot Instances: short workloads, cheap, can lose instance, enable to request unused instances, batch jobs
- Dedicated Hosts: book an entire physical server, controle instance placement. Allows to address compliance requirements and use existing server-bound software licences (on demand or reserved)
- Dedicated Instances: no other customers will share our hardware but others instances in same account use it
- Capacity reservations: reserve capacity in a specific AZ for any duration

**Shared Responsability Model for EC2:**
- AWS:
  - Infra and global network security
  - isolation on physical hosts
  - replacing faulty hardware
  - compliance validations
- Users:
  - Security Groups rules
  - OS patches and updates
  - software and utilities installed
  - IAM Roles assigned to EC2 & IAM user access management
  - data security

## EC2 Instance Storage

**EBS Volume:**

- Elastic Block Store Volume: network drive we can attach to our instances while they run, or also detach and attach to another (virtual hard disk in the cloud)
- block level storage
- allows instances to persist data, even after their termination
- can only be mounted to one instance at a time (at the CCP level) (but not for EBS Multi-Attach feature)
- bound to a specific availabilty zone, if we want to move in another AZ we need to snapshot it
- have a provisioned capacity, size un GBs, and IOPS (I/O operations per seconds) that we can upgrade
- one instance can have severall volumes

Delete on Termination attribute:
- controls the ebs behaviour when an EC2 instance terminates
- by default, root EBS is deleted but not others 

**Snapshots:**
- make a backup of EBS volume at a point of time
- recommended to detach the volume before
- they are stored on S3
- can copy accross AZ or Region
- snapshot will restore the EBS volume

Features:
- EBS Snapshot Archive: move a snap to an 'archive tier' (ebs snapshot archive), but it take 24 to 72 hours for restoring the archive
- Recycle Bin: retention from 1 day to 1 year

**AMI:**
Amazon Machine Image: Ready to use EC2 instances with our customizations

- customization of an EC2 instance (software, OS, config, monitoring, etc ..)
- faster boot/config time bc software is pre-packaged
- built for a specific region (and can be copied accross regions)
- launch EC2 instances from:
  - a public AMI: AWS provided (for ex Amazon Linux 2)
  - an own AMI: make and maintain ourself
  - an AWS Marketplace AMI (someone else made)
- AMI Process:
  - Start an EC2 instance and customize it
  - Stop the instance (for data integrity)
  - Build an AMI that will also create EBS snapshots
  - launch isntances from other AMIs

**EC2 Image Builder:**
- automated pipeline
- Used to automate the creation of VM or container images
- AUtomate the creation, maintain, validate and test EC2 AMIs:
  - Create a builder EC2 Instance that build components and applied (customize software on instance), then an AMI will be created, and after that the test suite is run by test EC2 instance. Finally, AMI is distributed (can be multiple regions)
- Can be run on a schedule

Recipe = Document that defines how the source image is going to be customized.

**EC2 Instance Store:**
- EBS volumes are network drives with "limited" performance, temporary block-level storage
- If we need a high-perf hardware disk, we use EC2 instance store (name of the hard drive attached to the physical server)
- better I/O perf
- lose their storage if they're stopped (instance store volumes ephemeral) or if hardware fails
- good for buffer, cache, temp content (informations that change frequently)

**EFS:**
- Elastic File System
- can be used with on-premises systems
- scale on demand to petabytes
- Third type of storage we can attach onto an EC2 instance
- managed NFS (network file system) that can be mounted on hundreds of EC2 instances
- works with Linux EC2 instances in multi AZ (can be mounted on instances accross multiple AZ)
- highly available, scalable, expensive, pay per use, no capacity planning
- all instances can mount the same EFS drive, using an EFS Mount Target and they will all see the same files

*EFS Infrequent Access (EFS-IA):*
- Storage class for EFS that is cost-optimized for files not accessed every day (up to 92% lower)
- EFS will automatically move files to EFS-IA based on the last time they were accessed
- enable EFS-IA with a Lifecycle Policy (for ex files not accessed for 60 days)

**Shared Responsability Model for EC2:**
- AWS responsibilities:
  - Infrastructure (global network security)
  - Replication for data for EBS volumes & EFS drives
  - replacing faulty hardware
  - ensuring their employees cannot access data
- User:
  - setting up backup/snapshot procedures
  - setting up data encryption
  - any data on the drives
  - understanding risk using ec2 instance store

**Amazon FSx:**
- launch 3rd party high-perf file systems on AWS
- fully managed service
- FSx Windows File Server: fully managed, highly reliable and scalable windows native shared file system:
  - built on windows file server
  - supports SMS protocol & windown NTFS
  - integrated with microsoft active directory
- FSx for Lustre:
  - fully managed, high-perf, scalable file storage for High Performance Computing (HPC)
  - machine learning, analytics, video processing, financial modeling, etc..
  - scales up to 100s GB/s, millions of IOPS, sub-ms latencies

## ELB & ASG

Elastic Load Balancing & Auto Scaling Groups 

**Scalabily:**
- app/sytem can handle greater loads by adapting, two kinds:
  - vertical scalability: increase size of the instance, the limit is the hardware -> scale up/down
  - horizontal scalability (= elasticity): for distributed systems, such as db, increase the number of instances/systems for the app -> scale out/in
-linked but different to high availability  
-> ability to accomodate a larger load by making the hardware strong (scale up) or by adding nodes (scale out)

**High availability:**
- running app/system in at least 2 AZ
- goes in  hand with horizontal scaling
- in order to survive a data center loss

**Elasticity:**
Once a system is scalable, elasticy means that there will be some "auto-scaling" so that the system can scale based on the load, it's "cloud-friendly" (pay per use, match demande, optimize costs)

**Agility:**
Not related to scalability, new IT resources are only a click away, which means reducing time to make those resources availables to developers from weeks to just minutes

**Load Balancer:**
- server that forward traffic to multiple servers (C2 instances) downstream
- spread load acrosse multiple downstream instances
- expose a single point of access (dns) to the app
- seamlessy handle failures of downstram instances
- do regular health checks to instances
- provide SSL termination (HTTPS) fro websites
- high availability across AZ

**ELB:**
- managed load balancer: AWS guarantees it will be working, takes care of upgradesn maintenance, high availability
- 3 kinds:
  - Application Load Blanacer (HTTP/HTTPS only) - Layer 7 (high-level protocol)
  - Network Load Balancer (ultra high perf, allows for TCP) - Layer 4 (lower level protocol)
  - Classic Load Balancer (slowly retiring) - Layer 4 & 7 at same time

**ASG:**
- allow to create and get rid of servers very quickly
- scale out (add EC2 instances) to match an increased load
- scale in (rmeove EC2 instances) to match a decreased load
- ensure we have a min/max of machines running
- auto register/deregister instances to load balancer
- replace unhealthy instances  
-> run at the optimal capacity

**Scaling Strategies:**
- Manual Scaling: update the size of an ASG manually
- Dynamic Scaling: repond to changing demand automatically:
  - simple/step scaling: when a cloudwatch alarm is triggered (for ex CPU >70%), then add 2 units, or remove if for ex CPU <30%
  - target tracking scaling: for ex i want the average asg cpu to stay around 40%
  - scheduled scaling: anticipate scaling based on known usage patterns
- Predictive Scaling:
  - uses machine laerning to predict future traffic ahead of time
  - auto provisions the right number of EC2 instances in advance  

## S3
*on premises* refers to local hardware, meaning data is stored on local servers, computers or other devices. For example, a company may purchase a server on which to store data. After buying the server, the company sets it up at their headquarters and uploads their data. Because the server is locally operated, it's considered on-premises data storage. 

**Use cases:**
- Back up and storage
- Disaster recovery
- Archive
- Hybrid Cloud Storage
- App, Media hosting
- Data lakes & big data analytics
- software delivery
- static websites

**Buckets:**
- Amazon S3 store object (files) in buckets (directories)
- must have a globally unique name (accross all regions all acounts)
- defined at the region level
- Naming convention:
  - no uppercase, no underscose
  - 3-63 characters long
  - not an IP
  - not start *with xn--* and not end with *-s3alias*

**Objects:**
- Have a key that is the FULL path (for s3://my-bucket/**my-folder-name/my-file.txt**, key is the bold text)
- key is composed from a prefix (folders) and object name (filename)
- there's no concept of directories, it's keys with very long names that contain slashes
- Object values are the content of the body:
  - max obj size is 5TB (5000GB)
  - if uploading more than 5GB, must use "multi-part upload"
- metadata about file (list of text key/value pairs)
- tags (unicode key/value pair - up to 10) - useful for security/lifecyle
- version ID (if versioning is enabled)

**Security:**
- User-Based:
  - IAM Policies: which API calls should be allowed for a specific user
- Resource-Based: 
  - Bucket Policies: bucket wide rules from the S3 console, allows cross account
  - Object Acess Control List (ACL)
  - Bucket Access Control List
- Encryption: encrypt objects using encryption keys

**Bucket Policy:**
- JSON based
- Used to:
  - grant public access to the bucket
  - force objects to be encrypted at upload
  - grant access to another account (cross account)

**Versioning:**
- it is enabled at the bucket level
- protct against unintended deletes (ability to restore a version)
- easy roll back to previous version
- any file not versioned will have version "null"
- suspending versionning does not delete the previous versions

**Replication:**
- CRR: Cross-Region replication
- SRR: Same_Region Replication
- Must enable versioning in source and destination buckets
- Buckets can be in diff AWS accounts
- Copying is asynchronous
- Must give proper IAM permissions to S3


**Storage Classes:**
- S3 can move between classes manually or using S3 Lifecycle config
- Durability (same for all classes) and Availability (varies on storage classes) 
- 99,999999999% durability
- store data in a flat non-herarchical structure

- General Purpose:
  - charges for data egress and per GB/month storage fee
  - Used for frequently accessed data
  - Big Data Analytics, mobile & gaming app, etc..
  - no retrieval fee
- Infrequent Access (IA):
  - less frequently accessed but requires rapid access when needed
  - disaster recovery, backups (standard infrequent access: S3 Standard-IA)
  - high durability in a single AZ, data lost when AZ is destroyed (S3 One-Zone IA), use for storing secondary backup copies 
- Glacier: 
  - low-cost object storage meant for archiving/backup
  - auto data encryption (AES-256)
  - Glacier Instant Retrieval: millisecond retrieval, min storage duration 90 days
  - Glacier Flexible Retrieval:  expedited (1 to 5 minutes), Standard (3 to 5 hours), Bulk (5 to 12 hours), min storage duration 90 days
  - Glacier Deep Archive: long term storage, satandard (12 hours), Bulk (48h), min storage 180 days (data accessed once or twice a year, backups & recovery)
- Intelligent Tiering: small monthly monitoring and auto-tiering fee, no retrieval fee, moves objects automatically between access tiers based on usage:
  - frequent access tier: default tier
  - infrequent access tier: obj not accessed for 30 days
  - archive instant access tier: objects not accessed for 90 days
  - archive access tier (opt): from 90 days to 700+ days
  - deep archive access tier (opt) from 180 days to 700+ days  

**S3 Encryption:**
- No encryption
- Server-side encryption: server encrypts the file after receiving it
- client-side encryption: encrypts the file before uploading it

**Shared Responsability Model for S3:**
- AWS responsibilities:
  - Infrastructure (global network security, availability)
  - config and vulnerability analysis
  - compliance validation
- User:
  - S3 versioning
  - bucket policies
  - replication setup
  - logging and monitoring
  - storage classes
  - data encryption

**AWS Snow Family:**
- Highly secure, portable devices to collect and process data at the edge, and migrate data into and out of AWS -> offline devices to perform data migrations (use if it takes more than a week to transfer over the network)
- Data migration: 
  - snowcone: small, portable computing, rugged and secured, used for edge computing, storage and data transfer (8TBs usable). Can be sent back to AWS offline or connected to the internet using AWS DataSync. Up to 24 TB 
  - snowball edge: move TBs or PBs of data in or out of AWS, pay per data transfer job, provide block storage and Amazon S3 compatible object storage (snowball edge storage optimized or snowball edge compute optimized, the two with HDD capacity) -> 80TB usable
  - snowmobile: transfer exabytes of data ( 1 EB = 1000 PB Petabytes = 1000000 TBs), each snowmobile has 100PB capacity. High security: temperature controlled, GPS, always under video surveillance 
- Edge computing: snowcone, snowball edge

**Edge Computing:**
- Process data while it's being created on an edge location, that is anything that doesn't really have internet (not or limited, for ex a ship on the sea, a mining station) or limited/no access to computing power
- Use cases are preprocess data, machine learning at the edge, transcoding media streams
- Snow Family:
  - snowcone: 2CPU, 4GB of memory, wired or wireless access, USB-C power
  - snowball edge - compture optimized: 52vCPU, 208GB of RAM, optional GPU, 42 TB usable storage
  - snowball edge - storage optimized: Up to 40vCPU, 80GB of RAM, object storage clustering available
-> All can run EC2 Instances & AWS Lambda functions (using AWS IoT Greengrass)

**Snow Family Usage Process:**

1. Request Snowball devices from the AWS console for delivery
2. Install the snowball client/AWS OpsHub on our servers
3. Connect the snowball to our servers and copy files using the lcient
4. Ship back the device 
5. Data will be loaded into an S3 bucket
6. Snowball is completely wiped

**AWS OpsHub:**
- to use snow family we need a CLI
- software to install on computer/laptop to manage snow family device

**AWS Storage Gateway:**
- Bridge between on-premise data and cloud data in S3
- Hybrid storage service to allow on-premises to seamlessly use the AWS Cloud
- Differents Types: File Gateway, Volume Gateway, Tape Gateway
- cannot be used for dara archival
- encryption auto enabled (using SSL)


## Databases & Analytics

**AWS RDS:**
- Relational Database Service
- used for OLTP workloads
- managed by AWS: automated provisioning, OS patching, continuous backups and restore to specific timestamp, multi AZ setup for DR (disaster recovery), scaling
- can't SSH into
- Postgres, MySQL, Aurora(AWS Proprietary db)
- better perf than a customer-managed db instance
- reserved instance pricing available
- can be reserved

**Amazon Aurora:**
- support postgreSQL and MySQL
- fully managed
- AWS cloud optimized, perf improvement
- storage automatically grow in increments of 10GB, up to 64TB

**RDS Deployment:**
- Read Replicas: 
  - scale the read workload of the DB
  - can create up to 5 replicas
  - writing is only done to the main db
- Multi-AZ:
  - Failover in case of AZ region outage (high availability)
  - Replication cross AZ
  - data is only written/read to the main db, and multi-az will be available only in case of an issue
  - only one other AZ as failover
- Multi-Region:
  - multi-regions (read replicas)
  - disaster recovery in case of region issue
  - local perf for global reads
  - cost

**ElastiCache:**
- Same way RDS is to get managed relational db but for Redis or Memcached
- in-memory db high perf, low latency
- reduce load off db for read intensive workloads
- can be reserved

**DynamoDB:**
- fully managed highly available replication accross 3 AZ
- no sql db
- scales to massive workloads, distributed "serverless" db
- millions of req per sec, trillions of row, 100s of TB storage
- single digit ms latency - low latency retrieval
- standard & Infrequent Acess (IA) table class
- key/value db
- can be reserved

**DynamoDB Accelerator - DAX:**
- Fully managed in memory cache for DynamoDB
- 10x perf improvement

**DynamoDB Global Tables:**
- make a dynamoDB table accessible with low latency in multiple regions
- users can read and write in any specific region
- active-active replication

**Redshift:**
- based on postgreSQL, but not used for OLTP (online transaction processing)
- OLAP (online analytical processing, computations, analytics and data warehousing)
- load data once every hour
- 10x better perf than other data warehouse, scale to PBs of data
- columnar storage of data
- massively parallel query execution (MPP), highly aailable
- pay as you go
- sql interface for performing the queries 
- BI (Business Intelligence) tools such as AWS Quicksight or Tableau integrated with it
- can be reserved

**EMR:**
- Elastic MapReduce
- helps creating Hadoop clusters (Big Data) to analyze and process vast amount of data
- clusters can be made of hundreds of EC2 instances
- takes care of provisionning and configuring all those EC2 instances so that they work together and can analyze data from a big data perspective
- auto-scaling and integrated with Spot Instances

**Athena:**
- serverless query service to perform analytics against S3 objects
- uses std SQL lgg to query the files
- supports CVS, JSON, ORC, Avro and Parquet (built on Presto engine)
- BI, analytics, logs, reporting, for ex for analyze data in S3 using serverless SQL

**QuickSight:**
- serverless machine learning-powered BI service to create interactive dashboards on the db
- fast, auto-scalling

**DocumentDB:**
- DocumentDB is an AWS implementation for MongoDB noSQL db like aurora for relationnal db
- mongoDB is used to store, query, and index JSON data
- similar deployment concepts as aurora
- auto scales to workloads with millions of req per seconds

**Neptune:**
- Fully managed graph db, for ex a popular dataset be a social network
- highly available accross 3AZ with up to 15 read replicas
- build and run app working with highly connected datasets - optimized for complex and hard queries
- can store billions of relations and query the graph ms latency

**QLDB:**
- Quantum Ledger Database
- A ledger is a book recording financial transactions
- fully managed db, serverless, high available, replicas accros 3 AZ
- review history of all the changes made to app data over time
- immutable system: no entry can be removed or modified, cryptographically verifiable (block hash)
- better perf than common ledger blockchain framework, manipulate data using SQL
- no decentralization concept, just a central db owned by amazon, in accordance with financial regulation rules

**Managed Blockchain:**
- Blockchain makes it possible to build app where multiple parties can execute transactions without the need for a trusted, central authority
- managed service to:
  - join public blockchain networks
  - create our own scalable private network
- compatible with the frameworks Hyperledger Fabric & Ethereum

**Glue:**
- managed extract, transform and load (ETL) service
- useful to prepare and transform data for analytics
- serverless service
- Glue Data Catalog: catalog of datasets that will have a reference of everything, the colum names, the field names, types, etc ... and can be use by services such as Athena, Redshift and EMR to discover the datasets and build the proper schemas for them

**DMS:**
- Database Migration Service
- quickly and securely migrate db to AWS, resilient, self healing
- the source db remain available during the migration
- supports:
  - Homogeneous migration for ex Oracle to Oracle
  - Heterogeneous migrations for ex microsoft sql server to aurora


## ECS, Lambda, Batch, Lightsail

**Docker:**
- software development platform to deploy apps
- apps are packaged in containers that can be run on any OS
- scale containers up and down very quickly
- on AWS, images can be stored in ECR (Elastic Container Registry), a private Docker registry that can be runned by ECS or Fargate (it store, manage and deploy)

**ECS:**
- Elastic Container Service
- Launch Docker containers
- must provision & maintain the infra (EC2 instances)
- AWS takes care of starting/stopping containers & has integrations with the App Load Balancer

**Fargate:**
- Launch Docker containers
- don't neeed to provision the infra
- serverless offering, AWS just runs container for us, based on the CPU/RAM we need

**Serverless:**
- new paradigm in which dev don't have to manage servers anymore (don't manage, provision or see), they just deploy code/functions
- Amazon S3, DynamoDB, Fargate, Lambda...

**Lambda:**
- FaaS: Function as a Service
- Regional scope
- virtual functions
- limited by time - short executions (up to 15 minutes)
- limited temporary disk space
- Event-Driven: run on-demand, get invoked by AWS when needed
- scaling automated
- pay per request/compute time
- lambda container image: the container image must implement the Lambda Runtime API (ECS/Fargate are preferred for running Docker images)
- NodeJS, Python, Java, C#, Golang, Ruby, custom runtime API (for ex Rust)

**API Gateway:**
- the API Gateway will proxy requests coming from client to lambda
- fully managed service to easily create, publish, maintain, monitor and secure APIs (serverless)
- supports RESTful APIs and WebSocket APIs, security, user auth, API throttling, API keys
- can be configured to send data directly to amazon Kinesis Data Stream

**Batch:**
Jobs that can run without end user interaction, or can be scheduled to run as resources permit, are called batch jobs. Batch processing is for those frequently used programs that can be executed with minimal human interaction. A program that reads a large file and generates a report, for example, is considered to be a batch job.
- enables developers, scientists, and engineers to easily and efficiently run hundreds of thousands of batch computing jobs on AWS
- fully managed batch processing at any scale
- run 100000s of computing 
- a "batch" job is a job with a start and an end (opposed to continuous)
- batch will dynamically launche EC2 instances or spot instances
- provisions the right amount of compute/memory
- we submit or schedule batch jobs and AWS Batch does the rest
- they are defined as Docker images and run on ECS
- no time limit
- any runtime
- rely on EBS/instance store for disk space
- relied on EC2 (managed service)

**Lightsail:**
- easiest way to launch and manage a virtual private server with AWS
- virtual servers, storage, db and networking (virtual private server, managed MySQL db)
- simpler alternative to using EC2, RDS, ELB, EBS, etc..
- setup notif and monitoring 
- simple web APP (MEAN, NodeJs for ex), websites (wordpress for ex), dev/test env
- high availability but no auto-scaling, limited AWS integrations
- for person with little cloud exp

## Deploying & Managing - Infra at scale

**Cloud Formation:**
- declarative way of outlining AWS infra, for any resource (define templates)
- CF creates those for us, in the right order, with the exact confi we specify
- Infra as code
- stack designer create a diagram with all resources and relations

**CDK:**
- define cloud infrastructure using a familiar lgg like JS, python, java and .NET
- the code is "compiled" into a CF template (JSON/YAML)
- can deploy infra and app runtime code together
- CDK App -> CDK CLI -> CF template -> CF

**Elastic Beanstalk:**
- Web App 3-tier: ELB -> EC2/ASG -> RDS/ElastiCache
- easy to use service free of cost, for deploying and scaling web apps and services (it provide server)
- upload code, then Elastic Beanstalk automatically handles the deployment, from capacity provisioning, load balancing, auto-scaling to application health monitoring
- developer centric view of deploying an app on AWS
- it uses EC2, ASG, ELB, RDS, etc..
- full control over the config
- PaaS, managed service
- just the app code is the responsability of the dev
- 3 archi models:
  - Single Instance deployment for dev
  - LB + ASG fro prod or pre-prod
  - ASG only: great for non-web apps in prod (workers)
- supports go, java, php, python, nodeJs, docker, etc..
- health monitoring:
  - full monitoring suite available
  - health agent pushes metrics to CW
  - ckecks for app health, published health events

**CodeDeploy:**
- deploy our app code automatically
- work with EC2 instances, Fargate, Lambda and on-premises servers -> hybrid service
- servers/instances must be provisioned and configured ahead of time with the CodeDeploy Agent

**CodeCommit:**
- source-control service that hosts Git-based repo
- codes changes are auto versioned

**CodeBuild:**
- code building service in the cloud
- compiles source code, run tests, and produce packages that are ready to be deployed
- fully managed and serverless

**CodePipeline:**
- orchestrate the different steps to have the code auto pushed to production, for exemple: code -> build -> test -> provision -> deploy
- basis for CICD
- fully managed 

**CodeArtifact:**
- software packages depend on each other to be built (code dependencies), and new ones are created
- artifact management = storing and retrieving these dependencies
- works with common dependency management tools such as npm, yarn, pip, etc..
- dev and codeBuild can retrieve dependencies from codeArtifact

**CodeStar:**
- unified UI to easily manage software dev activities in one place

**Cloud9:**
- cloud IDE fro writing, running and debugging code
- allow code collab in real-time

**Systems Manager (SSM):**
- gives visibility and control of your infrastructure on AWS
- operational insights of resources to quickly identify any issues that might impact applications using those resources
- provides a unified user interface so you can view operational data from multiple AWS services and allows you to automate operational tasks across your AWS resources
- allow to group resources
- helps manage and operate resources at scale
- helps manage EC2 and on-premises systems at scale -> hybrid service
- get operational insights about the state of the infra
- patching automation run commands accross an entire fleet of servers, store parameter config with SSM Parameter Store
- for Windows and Linux OS
- need to install SSM agent onto controlled systems, and use it to run commands, patch and config our servers

**SSM Session Manager:**
- allow to start a secure shell on EC2 and on-premises servers
- no ssh access, bastion hosts, or ssh keys needed, neither port 22
- supports Linux, MacOS and Windows
- send session log data to S3 or CW Logs

**OpsWorks:**
- configuration management service that provides managed instances of Chef and Puppet
- Chef & Puppet help config server auto, deploy, manage or perform repetitive actions (not created by AWS)
- work great with EC2 & on-premises VM
- OpsWork allow to managed Chef & Puppet (alternative to SSM)
- provision std AWS resources (db, elb, ebs volumes..)
- different OpsWork Layers
- can't be used for running commandes or managing patches on service, neither for provisioning AWS infra

## AWS Global Archi

**Global App:**
- deployed in multiple geogaphies
- decreased latency (time for a network packet to reach a server)
- disaster recovery
- attack protection

**Route 53:**
- managed DNS
- DNS is a collection of rules and records which helps clients understand how to reach a server through URLs
- IPv4 = A record / IPv6 = quadruple AAAA record / CNAME = hostname to hostname / hostname to AWS = Alias
- Policies:
  - Simple Routing Policy: no health checks (web browser to route 53)
  - Weighted Routing Policy: attribute % traffic on instances, health check
  - Latency Routing Policy: look where client is located, based on the latency
  - Failover Routing Policy: Primary EC2 instance and failover one, health check on the primary, in case of fail redirect to failover


**CloudFront:**
- Content Delivery Network (CDN)
- improves read perf by caching content at different edge locations, and content is served at the edge
- 216 points of presence (edge locations)
- great for static content that must be available everywhere
- DDoS protection, integration with Shield and AWS web application firawell
- cache from:
  - S3 bucket (enhanced security with CF Origin Access Identity OAI, CF can be used as an ingress)
  - Custom Origin (HTTP): ALB, EC2 instance, S3 website, or any HTTP backend

**S3 Transfer Acceleration:**
- increase transfer speed by transfering file to an AWS edge location which will fprward the data to the S3 bucket in the target region
- only for uploads and downloads

**AWS Global Accelerator:**
- improve global app availability and perf using the AWS global network -> optimize the route to the app (60% improvement)
- 2 Anycast Ip are created and the traffic is sent through edge locations
- integrated with AWS Shield
- no caching, proxying packets to app running in one or more AWS regions
- improves perf for a wide range of app over TCP/UDP
- good for non-http use cases
- provide static IP addresses that act as a fixed entrypoint to our app

**AWS Outposts:**
- "server racks" that offers the same AWS infra, services, APIs & tools to build our own app on premises just as in the cloud
- aws will setup and manage "outposts racks" within our on premises infra and we can start leverage AWS services on premises
- we are responsible for the physical security of the rack
- low latency, local data processing, data residency, easier migration, fully managed service
- with rack, can use EC2, EBS, S3, EKS, ECS, RDS, EMR..

**AWS WaveLength:**
- WaveLength Zones are infra deployments embedded within the telecommunication providers' datacenters at the edge of the 5G networks
- bring AWS services to the edge of 5G networks
- ultra-low latency
- traffic doesn't leave the Communication Service Provider's (CSP) network
- high bandwidth and secure connection to parent AWS Region
- for ex for connected vehicles, interactive live video streams, AR/VR, real-time gaming, smart cities..

**AWS Local Zones:**
- places aws compute, storage, db and other selected aws services closer to end users to run latency-sensitive apps
- extend VPC to more locations
- For ex AWS Region N.Virginia has AWS local zones Boston, Chicago, Dallas..

## Cloud Integration

There are two patterns of app communication:
- synchronous communications (app to app)
- asynchronous/event based (app to queue to app)

**SQS:**
- simple queue service
- producers send messages to the queue, and once messages are stored in a queue, then they can be red by consumers who will be polling the queue, that means requesting messages from the queue
- fully managed service (serverless), used to decouple app
- scales from 1 message per sec to 10000s
- default retention of messages: 4 days, maximum of 14 days
- no limit how many messages in the queue
- messages are deleted after they're read by consumers
- low latency

**Kinesis:**
- Kinesis = real-time big data streaming
- managed service to collect, process, and analyze real-time streaming data at any scale
- kinesis Data Streams: low latency streaming to ingest data at scale from hundreds of thousands of sources
- kinesis Data Firehose: load streams into S3, Redshift, ElasticSearch
- kinesis Data Analytics: perform real-time analytics on streams using SQL
- kinesis Video Streams: monitor real-time video streams for analytics or ML

**SNS:**
- simple notification service, pub/sub messaging service
- the "event publisher" only sends message to one SNS topic
- as many "event subscribers" as we want to listen to the SNS topic notifications, each subscriber will get all the messages
- subscribers can be SQS, lambda, kinesis data firehose, emails, sms & mobile notif, http(s) endpoints..
- enables you to decouple microservices, distributed systems, and serverless applications

**Amazon MQ:**
- SQS and SNS are "cloud-native" services: proprietary protocols from AS
- when migrating to the cloud, instead of re-engineering the traditional app to use SQS and SNS we can use Amazon MQ
- managed message broker service for:
  - RabbitMQ
  - ActiveMQ
- can run in multi-AZ with failover
- has both queue feature (~SQS) and topic features (~SNS)

## Cloud Monitoring

**CloudWatch:**
- provide metrics for every services in AWS
- metric = variable to montior (CPU utilization, NetworkIn..), they have timestamps
- monitor, store and access log files 
- also for on-premises servers
- CW billing metric data is stored in US East (N.Virginia) us-east-1

**CW Alarms:**
- used to trigger notif for any metric
- alarm actions:
  - auto-scaling: increase/decrease EC2 instances
  - ec2 actions: stop, terminate, reboot or recover
  - SNS notif: send a notif into an SNS topic
- can choose a period
- alarm states: OK/INSUFFICIENT_DATA/ALARM

**CW Logs**
- collect from apps (Elastic Beanstalk), containers (ECS), function, dns queries (Route53)
- CloudTrail based on filter
- CW log agents: on EC2 machines or on-premises servers for have logs (verify IAM permissions)
- real-time monitoring
- adjustable log retention

**EventBridge:**

- formerly CW Events:
  - schedule: cron jobs (scheduled scripts)
  - event pattern: event rules to react to a service doing something (for ex IAM root user sign in event)
- Default event Bus comes from AWS services, Partner event bus comes from AWS SaaS Partners, and Custom event bus comes from custom apps
- schema registry: model event schema
- we can archive events sent to an event bus, and replay them

**CloudTrail:**
- track user activity and detect unusual API usage
- provides governance, compliance and operational/risk audit for the AWS account
- get an history of events. Audit API calls made within account by Console, SDK, CLI and AWS services. Also identify user who temrinate an RDS DB instance for ex
- can put logs from CT to CW Logs or S3
- a trail can be applied to all regions (default) or a single one
- CT Insights:
  - automated analysis of CT Events
  - Raise alarms whenever the baseline resource numbers are crossed
  - helps AWS users identify and respond to unusual activity associated with write API calls by continuously analyzing CloudTrail management events

**X-Ray:**
- debug performance issues for a serverless application built using a microservices architecture
- tracing requests and visual analysis of our app
- troubleshooting perf (bottlenecks)
- understand dependencies in a microservice archi
- pinpoint service issues
- review request behavior
- find errors and exceptions
- look if we are meeting rime SLA (service-level agreement) -> are we replying on time to requests ?
- where it's throttled
- identify users that are impatced

**Code-Guru:**
- ML powered service for automated code reviews and app perf recommendations
- Reviewer: automated code reviews for static code analysis (dev)
- Profiler: visibilty/recommendations about app perf during runtime (prod), supports app running on AWS or on-premises
- supports java and python

**Service Health Dashboard:**
- show all regions and all services health
- RSS fee to subscribe to

**Personal Health Dashboard:**
- provides alerts and remediation guidance when AWS is experiencing events that may impact us

## VPC & Networking

**VPC:**
- private network to deploy resources in (regional resource)
- subnets allow to partition the network inside of our VPC (AZ resource), we can create one or more subnets within each AZ
- a public subnet is a subnet that is accessible from the internet
- a private subnet is a subnet not accessible from the internet
- to define access to the internet and between subnets we use Route Tables
- a vpc spans all of the AZ in the region, whereas a subnet spans only one AZ in the region

**Internet Gateway & NAT Gateways:**
- Internet Gateways helps our VPC instances to connect with the internet and public subnets have a route to the internet gateway
- NAT Gateways (AWS managed, created in public subnet) & NAT Instances (self-manged) allow instances in private subnets to access the internet while remaining private
- CIDR = range of IP 

**Network ACL & Security Groups:**
-  NACL is Ntwork Access Control List: 
  - firewall which controls traffic from and to subnet
  - have ALLOW and DENY rules that only include IP addresses  
  - attached at the subnet level
  - stateless: return traffic must be allowed by rules
- Security Groups:
  - firewall that controls traffic to and from an ENI (Elastic Network Interface)/EC2 Instance
  - only ALLOW rules that include IP addresses and other security groups
  - stateful : return traffic is auto allowed

**VPC Flow Logs:**
- capture info about IP traffic going into our interfaces
  - VPC Flow Logs
  - Subnet Flow Logs
  - Elastic Nextwork Interface Flow Logs
- help to monitor & troubleshoot connectivity issues
- captured network info from AWS managed interfaces like ELB, ElastiCache, RDS, Aurora...
- logs data can go to S3/CW Logs

**VPC Peering:**
- Connect two VPC and make them behave as if they were in the same network
- must not overlapping CIDC
- peering connection is not transitive

**VPC Endpoints:**
- endpoints allow to connect VPC to to AWS Services using a private network instead of the public www network
- better security and less latency
- VPC Endpoint Gateway: S3 & DynamoDB
- VPC Endpoint Interface: the rest (ENI)

**VPC Interface Endpoint:**
- elastic network interface with a private IP address from the IP address range of the subnet that serves as en entry point for traffic destined to a supported service
- powered by AWS PrivateLink

**PrivateLink:**
- VPC Endpoint Service family
- enables to privately access services by using private IP addresses
- most secure & scalable way to expose a service to 1000s of VPC (private network)
- does not require VPC peering, internet gateway, NAT, route tables..

**VPN:**
- Establish a secure network connection between on-premises network and AWS
- Site to Site VPN:
  - secure connection between on-premises VPN to AWS cloud resources 
  - connection auto encrypted
  - goes over the public internet
  - on premises it must use a Customer Gateway (CGW)
  - on AWS it must use a Virtual Private Gateway (VGW)
- Direct Connect (DX)
  - physical connection btw on-premises and AWS
  - private network
  - takes a month to establish the connection

**AWS Client VPN:**
- connect from our computer using OpenVPN to our private network in AWS and on-premises
- allow to connect to EC2 instances over a private IP

**Transit Gateway:**
- for having transitive peering between thousands of VPC and on-premises, hub-and-spoke (star) connection
- works with Direct Connect (direct private connection to AWS) Gateway, VPN connections

## Security & Compliance

**Shared Responsability Model:**
- AWS responsability - security **of** the Cloud:
  - protecting infra (hardware, software, facilities and networking) that runs all the AWS services
  - managed services like S3, DynamoDB..
- Customer Responsibility - security **in** the Cloud
  - For EC2 instance, management of the guest OS, firewall, network config, IAM
  - encrypted app data
- Shared controls:
  - patch management, config management, awareness & training

**DDoS Protection:**
- Distributed Denial-of-Service:
- AWS Shield Standard:
  - enabled for all AWS customers by default with no add cost
  - provides protection from attacks such as SYN/UDP Floods, Reflection attacks and other layer 3/4 attacks
  - protecrtion for EC2, CF
- AWS Shield Advanced: 
  - 24/7 premium DDoS protection, with response team (running on Route53 and Global Accelerator)
  - protect against more sophisticated attack 
- AWS WAF: 
  - can be used to protect on-premises resources if they are deployed behind an ALB
  - filter specific requests based on rules
  - protect from common web exploits (layer 7 -> HTTP)
  - on ALB, API Gateway, CF
  - define web ACL (rules based on IP addresses, HTTP headers, body and URI strings)
  - protects from common attacks like SQL injection and Cross-Site Scripting (XSS)
  - size constraints, geo-match (block countries)
  - rate-based rules (to count occurences of events) - DDoS protection
- CF and R53: availability protection, combined with AWS Shield, provides attack mitigation at the edge
- Be ready to scale - AWS auto-scaling

**Encryption:**
- 2 types:
  - at rest: data stored or archived on a device, for ex encrypted at rest on EFS/S
  - in transit: encryption while data is being moved from one place to another (in motion) 
- leverage encryption keys

**KMS:**
- Key Mangement Service
- AWS manages the encryption keys for us
- Encryption Opt-in: EBS volumes (encrypt volumes), S3 buckets (server-side encryption), etc..
- Encryption Auto enabled:CT Logs, S3 Glacier, storage gateway

**CloudHSM**:
- AWS provisions hardware device for any data encryption operations in the cloud, but we manage keys ourselves
- Dedicated hardware -> Hardware Security Module

**Customer Masters Keys (CMK):**
- Customer Managed CMK:
  - create, manage and used by the customer, can enable or disable
  - possibility of rotation policy
  - can bring our own key
- AWS managed CMK:
  - created, managed and used on the customer's behalf by AWS
  - used by AWS services
- AWS owned CMK:
  - collection of CMKs that an AWS service owns and manage to use in multiple accounts
  - AWS can use those to protect resources in our account (but we can't view them)
- CloudHSM Keys:
  - keys generated from our own CloudHSM hardware device
  - cryptographic operations are performed within the CloudHSM cluster

**AWS Certificate Manager (ACM):**
- let us easily provision, manage and deploy SSL/TLS certificates
- used to provide in-flight encryption for websites (HTTPS)
- supports public/private TLS certificates, auto renewal

**Secrets Manager:**
- for storing secrets
- capability to force rotation of secrets every X days
- automate generation of secrets (using lambda)
- integration with RDS
- encrypted by KMS
- rotate, manage and retreive db credentials, API keys, and others

**Artifact:**
- portal that provides customers with on-demand access to AWS compliance doc and agreements
- Artifact Reports 
- Artifact Agreements
- SOC reports (Service Organization Control), PCI reports (Payment Card Inudstry), BAA (Business Associate Addendum), NDA (Nondisclosure Agreement)


**GuardDuty:**
- intelligent threat discovery to protect AWS account
- use ML algo, anomaly detection, 3rd party data (CT event logs, VPC flow logs, DNS logs, EKS Audit Logs)
- can setup CW Event rules to be notified in case of findings that can target AWS lambda or SNS to do some actions
- can protect against CryptoCurrency attacks (dedicated "finding" for it)

**Inspector:**
- automated security assessments, for EC2 (SSM agent) and Containers push to ECR
- Reporting & integration with AWS Security Hub
- send findings to amazon event bridge
- continuous scanning of the infra, only when needed
- evaluates package vulnerabilities and network reachibility
- a risk score is associated with all vulnerabilities for prioritization

**Config:**
- fully managed service
- provides you with an AWS resource inventory, configuration history, and configuration change notifications to enable security and regulatory compliance
- enables you to assess, audit, and evaluate the configurations of your AWS resources
- helps with auditing and recording compliance of our AWS resources
- helps record config and changes over time
- possibility of storing the config data into S3 (analyzed by Athena)
- can receive alerts for any changes  (sns notif)
- per region service but can be aggregated across regions and accounts

**Macie:**
- fully managed data security and data privacy service that uses ML and pattern matching to discover and protect your sensitive data in AWS
- helps identify and alert to sensitive data such as personnaly identifiable (PII)
- Macie automatically provides an inventory of Amazon S3 buckets including a list of unencrypted buckets, publicly accessible buckets, and buckets shared with AWS accounts outside those you have defined in AWS Organizations

**Security Hub:**
- central security tool to manage security accross several AWS accounts and automate security checks
- collect potential issus & findings
- integrated dashboard showing current security and compliance status to quickly take actions
- auto aggregate alerts in predefined or personal findings formats from varous AWS services & AWS partner tools (GuardDuty, Inspector, Macie, IAM Access Analyzer, Systems Manager, Firewall Manager, Partner Network Solutions)
- must first enable AWS Config Service

**Amazon Detective:**
- analyzes, investigates and quickly identifies the root cause of security issus or suspicious activities (ML and graphs)
- auto collects ans processes events from VPC Flow Logs, CTrail, GuardDuty and create a unified view
- produces visualizations with detail sand context to get the root cause

**AWS Abuse:**
- report suspected AWS resources used for abusive or illegal purpose
- abusive & prohibited behaviors: spam, port scanning, DoS or DDoS attacks, intrusion attempts, hosting objectionable or copyrighted content, distributing malware

**Root User Privileges:**
- Change account settings
- view certain tax invoices
- close AWS account
- restore IAM user permissions
- change or cancel AWS support plan
- register as a seller in the Reserved Instance Marketplace
- config an S3 bucket to enable MFA
- edit or delete an S3 policy that includes an invalid VPC ID or enpoint ID
- sign up for GovCloud

## Machine Learning

**Rekognition:**
- Find objects, people, text, scenes and videos using ML
- Facial analysis and search to do user verification, people counting
- regional scope
- create a db of "familiar faces" or compare against celebrities

**Transcribe:**
- auto convert speech into text
- used a deep learning process called automatic speech recognition (ASR) to convert speech to text quickly and accurately
- can auto remove any PII using Redaction
- supports Automatic Language Identification 

**Polly:**
- TTS: Text-To-Speech
- Turn text into speech using deep learning
- allow to create app that talk

**Translate:**
- natural and accurate lgg translation
- allow to localize content such as websites and app for international users, and to easily translate large volumes of text efficiency

**Lex:**
- same techno that powers Alexa
- automatic pseech recognition (ASR) to convert speech to text (callers)
- natural lgg understanding to recognize the intent of text
- helps build chatbots, call center bots

**Connect:**
- receive calls, create contact flows, cloud-based virtual contact center
- can integrate with other Customer RelationShip (CRM) systems or AWS services

**Comprehend:**
- For Natural Language Processing (NLP)
- fully managed serverless service
- uses ML to find insights and relationships in text

**SageMaker:**
- fully managed service for dev/data scientists to build ML models
- helps with labelling, building, training, and tuning, deploy quickly

**Forecast:**
- fully managed service that uses ML to deliver highly accurate forecasts (for ex predict future sales of a raincoat)
- reduce forecasting time from months to hours

**Kendra:**
- fully managed document search service powered by ML
- extract answers from within a document (text,pdf...)
- natural lgg capabilities
- learn from user interactions/feedback to promote preferred results (incremental learning)
- ability to manually fine-tune search results

**Personalize:**
- fully managed ML service to build apps with real-time personalized recommendations
- same techno used by amazon.com
- can expose a customized personalized API

**Textract:**
- auto extracts text, handwriting, and data from any scanned documents using AI and ML
- extracts data from forms and tables
- read and process any type of documents

## Account Management, Billing & Support

**Organizations:**
- global service
- allows to manage multiple AWS accounts and automate the account creation processus
- main account is *master* account 
- cost benefits:
  - consolidated Biling across all accounts:
    - single payment method, one bill for multiple accounts
    - easy tracking of charges across accounts
    - share of volume pricing discounts, reserved instances and savings plans
    - no extra fee
  - pricing benefits from aggregated usage (volume discount for EC2, S3..)
  - pooling of reserved EC2 instances 
- API is available to automate AWS account creation
- restrict account privileges using Service Control Policies (SCP), govern access to aws services, resources and regions

**Multi-Account Strategies:**
- create accounts per department, cost center, dev/Test/prod, based on regulatory restrictions (using SCP), for better resource isolation (ex VPC), to have separate per-account service limits, isolated account for logging
- multi account vs one account multi VPC
- use tagging standard for billing purposes
- enable CT on all accounts, send logs to central S3 account
- send CW logs to center logging account

**Service Control Policies (SCP):**
- Whitelist or blacklist IAM actions
- appplied at the Organizational Unit or account level but not to the master account
- SCP is applied to all the Users and Roles of the Acccount, including Root, but does not affect service-linked roles
- SCP must have an explicit Allow (does not allow everything by default)
- used for example to restrict access to certain services (can't use EMR), enforce PCI compliance by explicitely disabling services
- inherit of allow/deny

**Org Consolidated Biling:**
- Combined usage accross all AWS accounts in the AWS Org to share the volume pricing, reserved instances and savings plans discounts
- One bill for all AWS accounts in AWS Org
- managment account can turn off reserved instances sharing for any account in the AWS Org including itself

**Control Tower:**
- easy wat to set up and govern a secure and compliant multi-account AWS env based on best practices
- automate the setup of env
- auto ongoing policy management using guardrails
- detect policy violations and remediate them
- monitor compliance through an interactive dashboard
- runs on top of AWS org (auto sets up AWS Org to organize accounts and implement SCPs)

**Pricing Models:**
- Pay as you go: pay for what you use, remain agile, meet scale demands
- Save when you reserve: minimize risks, predictably manage budgets, comply with long-terms requirements
- Pay less by using more: volume-based discounts
- Pay less as AWS grows
- use private IP instead of Public Ip for good savings and better network perf
- use same AZ for max savings

**Savings Plan:**
- commit a certain $ amount per hour for 1 or 3 years
- easiest way to setup long-term commitments on AWS
- EC2 Savings Plan: commit to usage of individual instance in a region (eg C5 or M5)
- Compute Savings Plan: regardless of family, region, size, os, tenancy, comptue options
- ML savings Plan: sagemaker...
- setup from AWS Cost Explorer console

**Credits:**
- applied in the following order:
  - soonest expiring
  - least number of applicable products
  - oldest credit

**Compute Optimizer:**
- Reduce costs and improve perf by recommending optimal AWS resources for workloads
- Help choose optimal config and right-size workloads (over/under provisioned)
- uses ML to analyze resources config and their utilization CW metrics
- support EC2 instances, ASG, EBS, Lambdas 
- recommendations can be exported to S3

**Billing & Costing Tools:**
- Estimating costs in the cloud, for our archi solution: Pricing Calculator
- Tracking costs in the cloud: 
  - Billing Dashboard (with Free Tier Dashboard usage)
  - Cost Allocation Tags: 
  - Cost and Usage Reports
  - Cost Explorer
- Monitoring against costs plans: Biling Alarms & Budgets

**Cost Allocation Tags:**
- used to tag and categorize resources and then run view the billing in Cost Explorer and the cost allocation report
- track AWS costs on a detailed level 
- AWS generated tags that automatically applied to the resource we create and start with rpefix *aws:* for ex *aws:createdBy*
- User-defined tags: defined by user and start with a prefix *user:* for ex *user:Stack*

**Tagging:**
- tags are used for organizing resources: EC2, RDS, VPC.. 
- Resources created by CF are all tagged the same way
- common tags are Name, Env, Team
- tags can be used to create Resource Groups (mange the tags using Tag Editor)
- for ex: to separate cost for AWS services by the department for cost allocation

**Cost & Usage Reports (CUR):**
- dive deeper into aws costs and usage, contains the most comprehensive set of AWS cost and usage data available, including additional metadata about AWS services, pricing, and reservations
- lists AWS usage for each service category used by an account and its IAM users in hourly or daily line items, as well as any tags that that we have activated for cost allocation purposes
- can be integrated and analyzed with Athena, Redshift or QuickSight

**Cost Explorer:**
- Visualize, understand, and manage AWS costs and usage over time
- create custom reports that analyze cost and uage data
- analyze data at high level: total costs and usage accross all accounts OR monthly, hourly, resource level granularity
- choose an optimal Savings Plan
- Forecast usage up to 12 months based on previous usage

**Billing Alarms in CW:**
- billing data metric is stored in CW us-east-1 and is agreggated for overall worldwide AWS costs
- actual costs, not for projected
- simple alarms

**Budgets:**
- Create budget and send alarms when costs exceeds the budget
- 3 types:
  - Usage
  - Cost
  - Reservation
- For reserved instances (RI): track utilization, supports EC2, elastiCache, RDS, Redshift
- up to 5 SNS notif per budget

**Trusted Advisor:**
- high level AWS account assessment
- analyze our account and provides recommendation on 5 categories:
  - cost optimization
  - performance
  - security
  - fault tolerance
  - service limits
- checks identify ways to optimize your AWS infrastructure, improve security and performance, reduce costs, and monitor service quotas
- for ex, warns when volumes (EBS)/EC2 instances are unused, or underused, identify if unrestricted access to resources has been allowed by SG

**TA - Support Plans:**
- 7 CORE checks (basic & dev support plan): S3 bucket permissions, security groups specific ports unrestricted, IAM Use (one IAM user mini), MFA on root account, EBS Public snapshots, RDS public snapshots, service limits
- FULL checks (business & ent support plan): full checks on the 5 categories, ability to set CW alarms when reaching limits, promgrammatic access using AWS Support API

**AWS Support Plans Pricing:**
- **Basic support:**
  - Customer Service & Communities - 24x7 access to customer service, doc, whitepapers and support forums
  - AWS Trusted Advisor: 7 core checks and guidance to provision resources following best practices to increase perf and improve security
  - AWS Personal Health Dashboard: peersonalized view of the health of AWS services, and alerts when our resources are impacted
- **Developer support plan:**
  - business hours email access to Cloud Support Associates (emailing AWS through opening support tickets in the console)
  - unlimited cases/ 1 primary contact
  - Case severity/response time (general guidance, system impaired)
- **Business Support Plan (24/7):**
  - used for prod workloads
  - technical support & architectural guidance contextual to specific use-cases
  - Trusted advisor full set of checks + API access
  - 24/7 phone, email and chat access to Cloud Support Engineers
  - unlimited cases/contacts
  - access to Infrastructure Event Management for add fee
  - case severity/response (+ prod system impaired/prod system down)
- **Enterprise On-Ramp Support plan (24/7):**
  - online training with self-paced labs
  - used for pord/business critical workloads
  - access to a pool of Technical Account Managers (TAM)
  - Concierge Support Team (for billing and account best practices or issues)
  - Infra Event Management, Well-Architected & Operations Reviews
  - case severity/response (+ business-critical system down <30 min)
- **Enterprise Support Plan (24/7):**
  - mission critical workloads
  - access to a designated Technical Account Manager (TAM
  - case severity/response (+ business-critical system down <15 min)
  
## Advanced Identity

**Security Token Service (STS):**
- enables to create temporary, limited-rpivileges credentials to access our AWS resources
- short-term credentials: config of expiration period
- uses cases: identity federation (for external systems), IAM Roles for cross/same account access, IAM Roles for EC2

**Cognito:**
- way to provide identity for web and mob app users (potentially millions) instead of creating them an IAM user, we create a user in Cognito
- own db of users with integrated login in mobile/web app
- supports sign-in with social identity providers like Apple, Google, FB, Amazon, and enterprise identity providers via SAML 2.0 (Security Assertion Markup Language) and OpenID Connect

**Microsoft Active Directory (AD):**
- found on ay Windows Server with AD Domain services
- db of objects: user accounts, computers, printers, file shares, security groups
- centralized security management, create account and assign permissions

**AWS Directory Services:**
- AWS Managed Microsoft AD: 
  - create our own AD in AWS, manage users locally, supports MFA
  - establish "trust" connections with our on-premises AD
- AD Connector:
  - directory Gateway (proxy) to redirect to on-premisesAD, supports MFA
  - users are managed on the on-premises AD
- Simple AD
  - AD compatible managed on AWS
  - cannot be joined with on-premises AD

**IAM Identity Center:**
- successor to AWS Single Sign-On
- centrally manage access to multiple AWS accounts and business applications and provide users with single sign-on access to all their assigned accounts and applications from one place
- one login (single sign-on) for all:
  - AWS accounts in AWS Organizations
  - Business cloud app (Salesforce, Box, Microsoft 365)
  - SAML2.0-enabled app
  - EC2 Windows Instances
- identity providers (where data is stored):
  - built-in identity store in IAM Identity Center
  - 3rd party: AD, OneLogin, Okta..

## Others services

**WorkSpaces:**
- managed desktop as a service (DaaS) solution to easily provision Windows or Linux desktops
- great to eliminate management of on-premises VDI (virtual desktop infrastructure)
- fast and quickly scalable to thousand of users
- secured data, integrated with KMS
- pay as you go service with monthly and hourly rates
- best practice is to deploy workspaces as close as users (as many workspaces regions as center locations to minimize latency)

**AppStream 2.0:**
- Desktop App Streaming Service, fully-managed non-persistent app and desktop streaming service
- deliver to any computer without acquiring and provisioning infra (no need to connect a VDI)
- the app is delivered from within a web browser and works with any device that has a web browser (devices/laptops)
- allow to config an instance type per app type (CPU, RAM, GPU)

**Sumerian:**
- create and run virtualy reality (VR), augmented reality (AR) and 3D apps
- can be used to quickly create 3D models with animations
- ready to use template and assets, no prog or 3D expertise required
- accessible via web-browser URLs or on popular hardware for AR/VR

**IoT Core:**
- "Internet of Things": the network of internet-connected  devices that are able to collect and transfer data
- allow to easily connect IoT devices to the AWS Cloud, for ex connected car, fridges, lights etc..
- serverless, secure & scalable to billions of devices and trillions of messages
- app can communicate with devices even if they aren't connected
- integrates with a lot of AWS services (lambda, sageMaker, S3..)
- build IoT app that gather, process, analyze and act on data

**Elastic Transcoder:**
- used to convert media files stored in S3 into media files in the formats required by consumer playback devices (phones, etc..) 
- it runs on a transcoding pipeline that will convert the file

**AppSync:**
- store and sync data accross mobile and web apps in real-time
- makes use of GraphQL (mobile techno from fb)
- client code can be generated automatically
- integrations with DynamoDB/Lambda
- real-time subscriptions
- offline data synchronization
- fine grained security

**Amplify:**
- framework that can leverage AWS AppSync
- set of tools that helps develop and deploy scalable full stack web and mobile app
- auth, storage, api, CI/CD, monitoring, source code...
- Amplify Studio for setup evreything we need, then Amplify is going to configure an Amplify back-end

**Device Farm:**
- fully-managed service that tests our web and mobile apps against desktop browsers, real mobile devices and tablets
- run tests concurrently on multiple devices (speed up exec)
- ability to config device settings (GPS, lggn Wi-Fi, bluetooth..)
- we can interact with devices and have reports, logs, screenshots..

**AWS Backup:**
- fully-managed service to centrally manage and automate backups accross AWS services
- on-demand and scheduled backups, create a Backup Plan
- supports PITR (point in time recovery -> restore db in 5 minutes)
- retention periods, lifecycle management, backup policies
- cross-region backup
- cross-account backup (using AWS organizations)

**Disaster Recovery Strategies:**
- Backup and Restore: 
  - cost minimum
  - data is backed up into the cloud and when there is a disaster we restore it somewhere else
- Pilot Light:
  - we have a cloud and we're going to run the core functions
- Warm Standby:
  - full version of the app ready in the cloud, but at minimum size
- Multi-Site/Hot-Site:
  - full version of the app, at full size
  - ready to be used
  - maximum cost
  
**AWS Elastic Disaster Recovery (DRS):**
- used to be named "CloudEndure Disaster Recovery"
- quickly and easily recover physicaln virtual and cloud-based servers into AWS
- for ex: protect most critical db, enterprise apps, protect data from ransomware attacks
- continuous block-level replication for servers from corporate data center into the cloud using DRS (into a staging), thanks to an AWS Replication Agent
- is disaster we can failover staging to production by creating bigger EC2 instances and EBS volumes
- when the corporate data center is back online, we can perfom a failback 

**AWS DataSync:**
- move large amount of data from on-premises to AWS
- can synchronize to S3, EFS, FSx for windows
- replication tasks can be scheduled hourly, daily or weekly and are incremental after the first full load (thanks to AWS DataSync Agent)

**AWS Application Discovery Service:**
- plan migration projects by gathering info about on-premises data centers
- server utilization data and dependency mapping, important for migrations
- Agentless Discovery (AWS Agentless Discovery Connector): VM inventory, config, and perf history such as CPU, memory, and disk usage
- Agent-based Discovery (AWS Application Discovery Agent): system config, perf, running processes, and details of the network connections btw systems
- resulting data can be viewed within AWS Migration Hub

**AWS Application Migration Service (MGN):**
- lift and shift (rehost) solution which simplify migrating app to AWS
- conerts physical, virutal and cloud-based servers to run natively on AWS
- continuous replication, then cutover from staging to production when ready to migrating

**AWS Fault Injection Simulator (FIS):**
- fully managed for running fault injection experiments on AWS workloads
- based on Chaos Engineering: stressing an app by creating disruptive events (eg sudden increase of CPU/memory), observing how the system reponds and implementing improvements
- help uncover hidden bugs and perf bottlenecks
- supports EC2n ECS, EKS, RDS...
- FIS create an experiment template to generate disruptions

**Step Functions:**
- lets you coordinate multiple AWS services into serverless workflows
- build serverless visual workflow to orchestrate our Lambda functions (can use AWS Glue and SageMaker too)
- design a graph and say at each step of the graph, in case of success or failure, what goes on next ?
- allow to have complex workflows within AWS
- features: sequence, parallel, conditions, timeouts, error handling..
- can integrate with EC2, ECS, on-premises servers, API gateway, SQS, etc..
- possibility of implementing human approval feature
- use cases: order fulfillment, data processing, web app, any workflow

**Ground Station:**
- fully managed service that lets us control sattelite communications, process data and scale satellite operations
- provides global network of satellite ground stations near AWS regions
- allow to download satellite data to our AWS VPC within seconds (in S3 or EC2)
- use cases: weather forecasting, surface imaging, communications, video broadcasts

**AWS Pinpoint:**
- scalable 2-way (outbound/inbound) marketing communicatiopn service
- supports email, SMS, push, voice, and in-app messaging
- ability to segment and personalize messages with the right content to customers
- possibility to receive replies
- scales to billion of messages per day
- for run campaigns by sending marketing, transactional SMS messages
- streams events (text_sucess, text_delivered..) to SNS, Kinesis Data Firehose, CW Logs
- create message templates, delivery schedules, full campaigns and highly-targeted segments

## Architecting & Ecosystem

**Well Architected:**
- Stop guessing capacity needs
- test systems at production scale
- automate to make architectural experimentation easier
- allow for evolutionary archi: design based on changing requirements
- drive archi using data
- improve through game days: simulate app for flash sales days (stressing the system)

**Design Principles:**
- Scalability: vertical & horizontal
- Disposable resources: servers should be disposable & easily configured
- Automation: serverless, IaaS, auto-scalling
- Loose Coupling: break the monolith down into smaller coupled components (a change or failure on one component should not cascade to the other)
- think Services, not Servers: don't just use EC2, use managed services, db, serverless..  
  
There are 6 pillars in the Well-Architected Tool:

**1. Operational Excellence**
- Includes the ability to run and montior systems to deliver business value and to continually improve supporting processes and procedures
- Design principles:
  - Perform operations as code: IaaS
  - anotate documentation
  - make frequent, small, reversible changes
  - refine operations procedures frequently and ensure that team members are familiar with it
  - anticipate failure and learn from all operational failures
- Steps:
  - Prepare: AWS CF, AWS Config
  - Operate: CF, Config, CloudTrail, CW, X-Ray
  - Evolve: CF, CodeBuild, CodeCommit, CodeDeploy, CodePipeline

**2. Security**
- Includes the ability to protect informations, systems and asserts while delivering business value through risk assessments and mitigation strategies
- Design principles:
  - implement a strong identity foundation (IAM, least privileges..)
  - enable traceability: integrate logs and metrics with systems to automatically repond and take action
  - apply security at all layers
  - automate security best practices
  - protect data in transit and at rest
  - keep people away from data
  - prepare for security events
- Services:
  - IAM: IAM, AWS-STS, MFA token, AWS organizations
  - Detective Controls: Config, CT, CW
  - Infra protection: CF, VPC, Shield, WAF, Inspector
  - Data protection: KMS, S3, ELB, EBS, RDS
  - Incident response: IAM, CF, CW Events

**3. Reliability**
- Ability of a system to recover from infra or service disruptions, dynamically acquire computing resources to meet demand, and mitigate disruptions such as misconfigurations or transient network issues
- Design principles: 
  - test recovery procedures
  - auto recover from failure
  - scale horizontally to increase aggregate system availability
  - stop guessing capacity
  - manage change in automation
- Services:
  - foundations: IAM, VPC, Service Limits (= service Quotas), Trusted Advisor
  - change management: Auto Scalling, CW, CT, Config
  - Failure management: Backups, CF, S3, S3 Glacier, Route 53

**Service Quotes (= Service Limits):** Service Quotas enables you to view and manage your quotas for AWS services from a central location. Quotas, also referred to as limits in AWS, are the maximum values for the resources, actions, and items in your AWS account. Each AWS service defines its quotas and establishes default values for those quotas.

**4. Performance Efficiency**
- Includes the ability to use computing resources efficiently to meet system requirements and to maintain that efficiency as demand changes and technologies evolve
- Design principles: 
  - democratize advanced technologies
  - go global in minutes
  - use serverless archi
  - experiment more often
  - mechanical sympathy: be aware of all AWS services
- Services:
  - Selection: Auto Scalling, Lambda, EBS, S3, RDS
  - Review: CF, AWS News Blog
  - Monitoring: CW, Lambda
  - Tradeoffs: RDS, ElastiCache, Snowball, CF

**5. Cost Optimization**
- Includes the ability to run systems to deliver business value at the lowest price point
- Design principles: 
  - adopt a consumption mode: pay only for what we use
  - measure overall efficiency
  - stop spending money on data centers operations
  - analyze and attribute expenditure
  - use managed and app level services to reduce cost of ownership
- Services:
  - expenditure awareness: Budgets, Cost and Usage Report, Cost Explorer, Reserved Instance Reporting
  - cost-effective resources: spot instances, reserved instance, S3 Glacier
  - matching supply and demand: Auto Scalling, Lambda
  - optimizing over time: Trusted Advisor, Cost and Usage Report, AWS News Blog

**6. Sustainability**
- Focuses on minimizing the environmental impacts of running cloud workloads
- Design principles: 
  - understand our impact: establish perf indicators and evaluate improvements
  - establish sustainability goals: set long-term goals for each workload, model return on investment (ROI)
  - maximize utilization
  - anticpate and adopt new, more efficient hardware and software offerrings
  - used managed services: shared services reduce the amount of infra, managed services help automate sustainability best practices as moving infrequent accessed data to cold storage and adjusting compute capacity
  - reduce the downstream impacy of our cloud workloads: reduce the amout of energy or resources required to use our services and reduce the need for our customers to updgrade their devices
- Services:
  - EC2 Auto Scaling, Serverless Offering (Lambda, Fargate)
  - Cost Explorer, AWS Graviton 2, EC2 T instances, spot instances
  - EFS-IA, S3 Glacier, EBS Cold HDD volumes
  - S3 Lifecycle Config, S3 Intelligent Tiering
  - Amazon Data Lifecycle Manager
  - Read Local, Write Global: RDS Read Replicas, Aurora Global DB, DynamoDB Global Table, CF

**AWS Well-Architected Tool:**
Free tool to review our archi against the 6 pillars Well-Architected Framework and adopt archi best practices

**Right Sizing:**
- EC2 has many instances types but choosing the most powerful isn't the best choice, bc the cloud is elastic
- right sizing = process of matching instance types and sizes to our workloads perf and capacity requirements at the lowest possible cost
- scaling up is easy so always start small
- also the process of looking at deployed instances and identifying opportunities to eliminate or downsize whithout compromizing capacity or other requirements, which results in lower costs
- important to right size before a Cloud Migration  nd continuously after the cloud onboarding process (reuqirements change over time)
- CW, Cost Explorer, Trusted Advisor, 3rd party tools can help

**AWS Ecosystem:**
- AWS Blogs
- AWS Forums (community)
- AWS Whitepapers & Guides: for example the well architected framework
- AWS Quick Starts:
  - automated, glob-standard deployments in the AWS Cloud
  - quickly deploy a popular technology on AWS
  - build a prod env quickly with templates
  - leverages CF
- AWS Solutions: vetted technology solutions for the AWS Cloud (for ex AWS Landing Zone, replaced by AWS Control Tower)
- AWS Support
- AWS Marketplace: digital catalog with thousands of software listings from independent software vendros (3rd party)
- AWS Training:
  - AWS Digital (online) and Classroom Training (in-person or virtual)
  - AWS Private Training (for organization)
  - Training and Certification for the US Government
  - Training and Certification for the Enterprise
  - AWS Academy: helps universities teach AWD
- AWS Professional Services organization: 
  - global team of experts
  - They work alongside our team and a chosen member of the APN
  - APN = AWS Partner Network:
    - APN Technology Partners: providing hardware, connectivity and software
    - APN Consulting Partners: profesional services firm to help build on AWS
    - APN Training Partners: find who can help us learn AWS
    - AWS Competency Program: granted to APN Partners who have demonstrated technical proficiency and proven customer success in specialized solution areas
    - AWS Navigate Partner: train the Partners

**AWS Knowledge Center:**
Contains the most frequent & common questions/requests.

**AWS IQ:** 
- Quickly find a professional help for our AWS projects 
- Engage and pay AWS Certified 3rd party experts for on-demand project work
- video-conferencing, contract management, secure collab, integrated billing
- for customers: 
  - submit request: describe project
  - review responses: connect to experts
  - select expert: based on rates, experience
  - work securely: give experts appropriate access to AWS account
  - pay per milestone: charges added into AWS Bill
- for experts:
  - create profile: photo, bio, certs...
  - connect with customers
  - start a proposal: work desc, price, milestones
  - work securely: get appropriate access
  - get paid: after milestones are met

**AWS re:Post:**
- community forum
- AWS managed Q&A service offering crowd-sourced, expert reviewed answers to our technical questions about AWS that replaces the original AWS Forums
- community members can earn reputation points to build up their community expert status by providing accepted answers and reviewing answers from other users
- questions from AWS premium support customers that do not receive a response from the community are passed on to AWS Support engineers
- not for questions time-sensitive or involve any proprietary info
