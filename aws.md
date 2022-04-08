# 35 classes and 18 AWS services with LAB:
- Intro to Cloud
- Intro Linux and apache server
- Intro to AWS and AWS Services:
    1. Amazon Snow Family
    1. AWS Identity and Access Management (IAM)
    1. Amazon S3
    1. Amazon CLI
    1. Amazon EC2
    1. Amazon Elastic Block Store (Amazon EBS)
    1. Amazon Elastic File System (Amazon EFS)
    1. Elastic Load Balancing
    1. AWS Auto Scaling
    1. Amazon CloudWatch
    1. Amazon Route 53
    1. Amazon Simple Notification Service (Amazon SNS)
    1. Amazon Simple Queue Service (Amazon SQS)
    1. Amazon VPC (and associated features)
    1. Amazon RDS
    1. Amazon CloudFront
    1. AWS Lambda
    1. AWS Elastic Beanstalk
    1. AWS CloudFormation
- Project 1 involves EC2 and Well Architecture FrameWork
- Project 2 involves VPC and CloudFormation
#
1. AWS Snow Family
    - How do we do Migration to AWS
    - What is Snow Family
1. AWS Identity and Access Management (IAM)
    - What is IAM
    - Building Blocks of IAM
    - LAB:
        - Initial Setup and Configuration
        - Creating an IAM User
        - Creating an IAM Group and Attach User
        - Creating/Addiding an IAM Policy & attach to user/group
1. Amazon S3
    - Buckets and Objects
    - Storage Classes
    - Object Lifecycles Management
    - Permissions & Object Versioning
    - Static Web Hosting with S3 Bucket
    - LAB:
        - Creating and Deleting buckets
        - Adding objects to buckets and deleting
        - Making the buckets and objects to be public
        - Versioning the buckets
        - Delete marker to restore the versioning
        - Create a LifeCycle Management
        - Cross Replication buckets
        - Adding encryption to objects
        - Create a Static website using S3.
1. Amazon CLI
    - Why CLI
    - How to configure CLI
    - What is IAM Role
    - LAB:
        - Create a user with Programmatic access
        - Install AWS CLI and configure Access ID
        - Creating an IAM Role for S3 access
        - Connecting via AWS CLI to creates s3 buckets
1. Amazon EC2
    - EC2 Basics
    - Instance Types
    - Security Groups
    - Launching and Using an EC2 instance (Windows instance & Linux Instance)
    - EC2 Bootstrapping, User Data, and Meta Data
    - Key pair and connecting to an EC2 via SSH & RDP
    - EC2 Placement Groups
    - Status Checks
    - LAB:
        - Create a Amazon EC2 server
        - Different ways to SSH and configure
        - Create/Run apache server in local system and EC2 instance
        - Bootstrap code and metadata in EC2
1. Amazon Elastic Block Store (Amazon EBS)
    - Elastic Block Store and Types
    - Analogy of throughput and Iops
    - Volumes and snapshots
    - Encryption and Hibernation
    - LAB:
        - Creating and deleting volumes
        - Attaching and detaching volumes
        - Mounting and Unmounting the attached volume
        - Creating snapshots & Usage of snapshots
        - Increasing the volume size
        - Encrypting the volumes
        - Hibernation and stop start difference
1. Amazon Elastic File System (Amazon EFS)
    - What is EFS and its use case
    - When to use EFS
    - LAB:
        - Create EFS
        - Create a Security Group with NFS port
        - Create two EC2 instances
        - Configure EFS and create sample data in that folder 
1. Elastic Load Balancing
    - Elastic Load Balancing and Types
    - Load Balancer Components
    - Health Check Status
    - Listeners and Target Groups
    - Rules
    - Sticky Sessions and De-registration delay
    - LAB:
        - Creating Target Groups
        - Adding Instances to TG
        - Create a Application LoadBalancer
        - Experience the traffic balanced by ELB in Realtime.
1. AWS Auto Scaling
    - What is Autoscaling and types of Scaling?
    - Launch Template and AutoScaling Group
    - Group Size and Polices
    - Auto Scaling Components
    - LAB:
        - Create a Launch Template 
        - Launch a instance via Launch Template
        - How to Setup and Use Auto Scaling
        - Change group sizes and experience the reflected isntances
        - Using Auto Scaling with Elastic Load balancer (ELB)
1. Amazon CloudWatch
    - Monitoring with Cloud watch
    - Getting statistics for a specific EC2 instance
    - Configure AWS cloud watch agent
    - Cloud Watch Create a Alaram to email
1. Amazon Route 53
    - Registering a Web Domain
    - DNS and record types
    - Configuring Route 53 to use a domain
    - Health Checks with EC2 
    - R53 different policy
1. Amazon Simple Notification Service (Amazon SNS)
    - SNS Components & Usage
    - LAB:
        - Creation of a topic
        - Subscribing to topic via Email
        - Setting notification for EC2 instance changes
1. Amazon Simple Queue Service (Amazon SQS)
    - Usage of SQS
    - SQS Types
    - LAB:
        - Creation of SQS
        - Sending messages to the queue



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









1. Amazon RDS
1. Amazon CloudFront
    - What is Cloud Front
    - Edge Location, Distribution, Origin, CDN,TTL (Time To Live)
    - Invalidations
    - LAB:
        - Create a S3 with static website
        - Create Cloud Front
        - Attach CloudFront to S3
1. AWS Lambda
1. AWS Elastic Beanstalk
1. AWS CloudFormation
    - Benefits of Infrastructure as a code
    - Introduction to Designer Template
    - Introduction to JSON & YAML
    - LAB:
        - Create an S3 & EC2 using IAAC








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