Snow	: 21
IAM 	: 04
S3 		: 05
EC2 	: 06
EBS		: 07
EFS		: 07
ELB		: 11
Watch	: 12
ASG-EC2 : 13
RDS		: 08
CFront	: 19
VPC		: 09
R53		: 10
SQS		: 14
SNS		: 14
Lambda	: 16
Beansta	: 18
Formatn	: 18

# 35 classes and 18 AWS services with LAB:
- Intro to Cloud
- Intro Linux and apache server
- Intro to AWS and AWS Services:
    1. Amazon Snow Family
    1. AWS Identity and Access Management (IAM)
    1. Amazon S3
    1. Amazon EC2 and CLI
    1. Amazon Elastic Block Store (Amazon EBS)
    1. Amazon Elastic File System (Amazon EFS)
    1. Elastic Load Balancing
    1. Amazon CloudWatch
    1. AWS Auto Scaling
    1. Amazon RDS
    1. Amazon CloudFront
    1. Amazon VPC (and associated features)
    1. Amazon Route 53
    1. Amazon Simple Notification Service (Amazon SNS)
    1. Amazon Simple Queue Service (Amazon SQS)
    1. AWS Lambda
    1. AWS Elastic Beanstalk
    1. AWS CloudFormation
- Project 1 involves EC2 and Well Architecture FrameWork
- Project 2 involves VPC and CloudFormation

#
1. Amazon EC2 and CLI
    - EC2Basics
    - Amazon Machine Images(AMIs)
    - What is AMI
    - Choosing & Working with AMIs
    - Creating your own AMI/Registering your own AMI
    - Sharing/Copying AMI to other AWS accounts
    - Instance Types
    - On-demand  instances, Spot  instances, Reserved instances
    - Elastic Block Store (EBS)
    - Creating and deleting volumes             
    - Attaching and detaching volumes
    - Mounting and Unmounting the attached volume
    - Creating snapshots & Usage of snapshots
    - Increasing the volume size
    - Security Groups
    - IP Addressing
    - Launching and Using an EC2 instance (Windows instance & Linux Instance)
    - EC2 Bootstrapping, User Data, and Meta Data
    - Key pair and connecting to an EC2 via SSH & RDP
    - EC2 Placement Groups
1. Amazon Elastic Block Store (Amazon EBS)
1. Amazon Elastic File System (Amazon EFS)
1. Amazon VPC (and associated features)
    - VPC Basics
    - Internet Gateways (IGW)
    - Route Tables (RTs)
    - Network Access Control List (NACLs)
    - Subnets
    - Availability Zones (VPC Specific)
    - LAB:
        - Creating a custom VPC
        - Setting up internet access for virtual machines
        - Create Route Table, NACL, Subnets and connect them
1. Amazon Route 53
    - Route 53 Basics
    - Route 53 Definition
    - DNS servers
    - Understanding how web servers are located
    - Registering a Web Domain
    - Configuring Route 53 to use a domain
1. Elastic Load Balancing
    - Introduction to Elastic Load Balancing
    - Benefits and ELB Use Cases
    - Pricing/Cost Overview
    - ELB Security
    - Communication Protocols
    - LAB:
    - Create a Classic ELB
        - Adding Instances to ELB
        - Experience the traffic balanced by ELB in Realtime.



















1. Introduction to Cloud Computing
    - Why Cloud Computing
    - What is Cloud Computing
    - Cloud Providers
1. Cloud Computing Models
    - Deployment Models
        - Public Cloud
        - Private Cloud
        - Hybrid Cloud
    - Service Models:
        - Infrastructure as a Service (IaaS)
        - Platform as a Service (PaaS)
        - Software as a Service (SaaS)
1. Introduction to Amazon Web Services:
    - Why AWS
    - What is AWS
    - Who is using AWS
    - AWS Advantages
    - AWS Service Catalog/Framework
    - AWS Global Infrastructure
    - Regions and Availability Zones – How to choose the right one
    - Domains of AWS
1. AWS Subscription & Overview
    - Subscription to AWS
    - AWS Free tier – Limits and usage
    - Introduction to the AWS Management Console
1. Cloud Watch Create a Alaram to email
1. Simple Storage Service (S3)
    - S3 Basics
    - Buckets and Objects
    - Storage Classes
    - Object Lifecycles Management
    - Permissions & Object Versioning
    - Static Web Hosting with S3 Bucket
    - LAB:
        - Creating and Deleting buckets
        - Adding objects to buckets
        - Getting & Deleting objects
        - Making the buckets and objects to be public
        - Adding security to objects
        - Versioning the buckets
        - Delete marker to restore the versioning
        - Create a LifeCycle Management
        - Cross Replication buckets
        - Create a Static website using S3.
1. Amazon CloudFront
    - What is Cloud Front
    - Edge Location, Distribution, Origin, CDN
    - Invalidations
    - LAB:
        - Create Distribution
        - Attach CF to S3
1. AWS Snowball
    - What is Snowball
    - How to use snowball and small LAB demo
1. AUTO SCALING
    - What is Autoscaling?
    - Conceptual overview of Auto Scaling
    - Auto Scaling Components
    - Pricing/Cost Overview
    - Launch Configurations
    - Auto Scaling Groups
    - LAB:
        - How to Setup and Use Auto Scaling
        - Using Auto Scaling with Elastic Load balancer (ELB)
1. CLOUD WATCH
    - CloudWatch States
    - Monitoring with Cloud watch
    - Getting statistics for a specific EC2 instance
    - Getting aggregated statistics
1. CLOUD FORMATION(IAAC)
    - Benefits of Infrastructure as a code
    - Introduction to Designer Template
    - Introduction to JSON & YAML
    - LAB:
        - Create an S3 & EC2 using IAAC
1. Identity and Access Management (IAM)
    - What is IAM
    - Multifactor Authentication
    - IAM initial setup and configuration
    - IAM users and policies
    - IAM groups and policies
    - IAM Roles
    - IAM Programmatic access
    - Creating an IAM Policy
    - LAB:
        - Creating an IAM User
        - Creating an IAM Group
        - Creating an IAM Role & connecting via AWS CLI
        - Creation of Custom Policies
1. SIMPLE NOTIFICATION SERVICE(SNS)
    - SNS Components & Usage
    - LAB:
        - Creation of a topic
        - Subscribing to topic via Email
        - Setting notification for EC2 instance changes 
1. Cloud Front
    - What is Cloud Front
    - Setting up of Cloud Front
    - Architecture of Cloud Front
    - Content delivery network (CDN)
    - Edge Locations
    - Origin
    - Distribution
    - TTL (Time To Live)
1. SIMPLE QUEUE SERVICE(SQS)
    - Usage of SQS
    - SQS Types
    - LAB:
        - Creation of SQS
        - Sending messages to the queue
1. Disaster Recovery