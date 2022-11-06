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