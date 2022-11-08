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
- Trade capital expense (CAPEX) for operational expense (OPEX): pay on demand, reduce total cost of ownership (TCO) & Operational Expense (OPEX)
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
  - Compliance with data governance and legal requirements: data never leaves a regio without explicit permission
  - Proximity to customers: reduced latency
  - Available services within a Region
  - Pricing: varies region to region
- AWS Availabality Zones: usually 3, min is 2 and max is 6 (for ex ap-southest-2a, ap-southest-2b). Separate from each other, discrete data centers with redundant power, networking and connectivity. They are connected with high bandwidth and ultra-low latency. Link together, they will form a region.
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
  - Universal 2nd factor (U2F) Security Key: physical device like YubiKey (3rd party), support multiple root and IAM users 
  - Hardware Key Fob MFA Device 
  - Hardware Key Fob MFA Device for AWS GovCloud (US)

**IAM Roles for Services:**
- some AWS services will need to perform actions on our behalf
- we'll assign permissions to AWS services with IAM roles
- for ex, EC2 Instance Roles, Lambda Function Roles, etc...

**Security Tools:**
- IAM Credentials Report (account-level): a report that lists all our account's users and the status of their various credentials
- IAM Access Advisor (user-level):  shows the service permissions granted to a user and when those services where last accessed, it can be use to revise policies

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
- Spot Instances: short workloads, cheap, can lose instance
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

- Elastic Block Store Volume: network drive we can attach to our instances while they run, or also detach and attach to another
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
- EBS volumes are network drives with "limited" performance
- If we need a high-perf hardware disk, we use EC2 instance store (name of the hard drive attached to the physical server)
- better I/O perf
- lose their storage if they're stopped (ephemeral) or if hardware fails
- good for buffer, cache, temp content

**EFS:**
- Elastic File System
- Third type of storage we can attach onto an EC2 instance
- managed NFS (network file system) that can be mounted on hundreds of EC2 instances
- works with Linux EC2 instances in multi AZ
- highly available, scalable, expensive, pay per use, no cpacity planning
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
- high availability across zones

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

- General Purpose:
  - Used for frequently accessed data
  - Big Data Analytics, mobile & gaming app, etc..
- Infrequent Access (IA):
  - less frequently accessed but requires rapid access when needed
  - disaster recovery, backups (standard infrequent access: S3 Standard-IA)
  - high durability in a single AZ, data lost when AZ is destroyed (S3 One Zone-IA), use for storing secondary backup copies 
- Glacier: 
  - low-cost object storage meant for archiving/backup
  - Glacier Instant Retrieval: millisecond retrieval, min storage duration 90 days
  - Glacier Flexible Retrieval:  expedited (1 to 5 minutes), Standard (3 to 5 hours), Buk (5 to 12 hours), min storage duration 90 days
  - Glacier Deep Archive: long term storage, satandard (12 hours), Bulk (48h), min storage 180 days
- Intelligent Tiering: small monthly monitoring and auto-tiering fee, moves objects automatically between access tiers based on usage:
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
- software to install on copputer/laptop to manage snow family device

**AWS Storage Gateway:**
- Bridge between on-premise data anc cloud data in S3
- Hybrid storage service to allow on-premises to seamlessly use the AWS Cloud
- Differents Types: File Gateway, Volume Gateway, Tape Gateway


## Databases & Analytics

**AWS RDS:**
- Relational Database Service
- used for OLTP workloads
- managed by AWS: automated provisioning, OS patching, continuous backups and restore to specific timestamp, multi AZ setup for DR (disaster recovery), scaling
- can't SSH into
- Postgres, MySQL, Aurora(AWS Proprietary db)

**Amazon Aurora:**
- support postgreSQL and MySQL
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

**DynamoDB:**
- fully managed highly available replication accross 3 AZ
- no sql db
- scales to massive workloads, distributed "serverless" db
- millions of req per sec, trillions of row, 100s of TB storage
- single digit ms latency - low latency retrieval
- standard & Infrequent Acess (IA) table class
- key/value db

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
- massively parallel query execution (MPP), higly aailable
- pay as you go
- sql interface for performing the queries 
- BI (Business Intelligence) tools such as AWS Quicksight or Tableau integrated with it

**EMR:**
- Elastic MapReduce
- helps creating Hadoop clusters (Big Data) to analyze and process vast amount of data
- clusters can be made of hundreds of EC2 instances
- takes care of provisionning and configuring all those EC2 instances so that they work together and can analyze data from a bid data perspective
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

**QLBD:**
- Quantum Ledger Database
- A ledger is a book recording financial transactions
- fully managed db, serverless, high available, replicas accros 3 AZ
- review history of all the changes made to app data over time
- immutable system: no entry can be removed or modified, cryptographically verifiable (block hash)
- better perf that common ledger blockchain framework, manipulate data using SQL
- no decentralization concept, just a central db owned by amazon, in accordance with financial regulation rules

**Managed Blockchain:**
- Blockchain makes it possible to build app where multiple parties can execute transactions without the neer for a trusted, central authority
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
- on AWS, images can be stored in ECR (Elastic Container Registry), a private Docker registry that can be runned by ECS or Fargate

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
- fully managed serviceto easily create, publish, maintain, monitor and secure APIs
- supports RESTful APIs and WebSocket APIs, security, user auth, API throttling, API keys

**Batch:**
Jobs that can run without end user interaction, or can be scheduled to run as resources permit, are called batch jobs. Batch processing is for those frequently used programs that can be executed with minimal human interaction. A program that reads a large file and generates a report, for example, is considered to be a batch job.
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
- virtual servers, storage, db and networking
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
- deploy our app automatically
- work with EC2 instances and on-premises servers -> hybrid service
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
- helps manage E2 and on-premises systems at scale -> hybrid service
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
- Chef & Puppet help config server auto or perform repetitive actions (not created by AWS)
- work great with EC2 & on-premises VM
- OpsWork allow to managed Chef & Puppet (alternative to SSM)
- provision std AWS resources (db, elb, ebs volumes..)
- different OpsWork Layers

## AWS Global Archi

**Global App:**
- deployed in multiple geogaphies
- decreased latency (time for a network packet to reach a server)
- disaster recovery
- attack protection

**Route 53:**
- managed DNS
- DSN is a collection of rules and records which helps clients understand how to reach a server through URLs
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
- DDoS protection, integration with Shield and AWS web application firewell
- cache from:
  - S3 bucket (enhanced security with CF Origin Access Identity OAI, CF can be used as an ingress)
  - Custom Origin (HTTP): ALB, EC2 instance, S3 website, or any HTTP backend

**S3 Transfer Acceleration:**
- increase transfer speed by transfering file to an AWS edge location which will fprward the data to the S3 bucket in the target region
- only for uploads and downloads

**AWS Global Accelerator:**
- improve global app availability and perf using the AWS global network -> optimize the route to the app (60% improvement)
- 2 Anycast Ip are created and the traffic is sent through edge locations
- integrated ith AWS Shield
- no caching, proxying packets to app running in one or more AWS regions
- improves perf for a wide range of app over TCP/UDP
- good for http that require static IP address

**AWS Outposts:**
- "server racks" that offers the same AWS infra, services, APIs & tools to build our own app on premises just as in the cloud
- aws will setup and manage "outposts racks" within our on premises infra and we can start leverage AWS services on premises
- we rare responsible for the physical security of the rack
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