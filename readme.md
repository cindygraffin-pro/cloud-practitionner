# AWS Cloud Practitioner

Cloud Practitioner exam - CLF-C01

## Cloud Computing

**How the web works ?**

The client will use the network to route the packets, the data into the server, then the server will rpely to us and we will get the response.  
Client and server have an IP address that allow each one to reach other.

**What is a server composed of ?**
- CPU: little piece that do some computations, it do some calculations and find results
- RAM: Fast memory, allow to store and fin information fastly
CPU + RAM = like a brain
- Storage Data (for ex files)
- Database: store data in a structured way
- Network: cables, routers and servers connected with each other (routers, switch, DNS server)

Router = networking device that forwards data packets between computer networks  
Switch = tkaes a packet and send it to the correct server/client on the network

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


