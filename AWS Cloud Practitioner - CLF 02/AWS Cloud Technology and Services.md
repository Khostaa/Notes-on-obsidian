## Amazon Elastic Compute Cloud (EC2) 
- Amazon Elastic Compute Cloud, or EC2, provides scalable compute capacity in AWS. 
- Each EC2 machine, called an instance, can scale based on your requirements.
### Key Characteristics
- ability to scale up or down based on demand.
- availability of varied range of instance types for specialized use cases.

- AWS offers various instance types optimized for different use cases, and EC2 instances integrate seamlessly with other AWS services like storage, databases, and networks.
![[ec2 with various services.png]]
### EC2 instance types
- offers six categories of EC2 instances for specialized workloads.
	- General purpose
	- Compute optimized
	- Memory optimized
	- Storage optimized
	- Accelerated computing
	- High performance Computing (HPC) optimized
#### General Purpose instances
- Balance of compute, memory, and networking resources
- use cases:
	- hosting dynamic websites
	- maintaining code repositories
#### Storage Optimized instances
- high, sequential read and write access to large datasets
- use cases:
	- Data warehousing
	- Refactoring large relational databases
#### Compute Optimized instances
- Compute-intensive and high-performance workloads
- Use cases:
	-  Scientific simulations
	-  Financial modeling
#### Memory Optimized instances
- Memory-intensive workloads not requiring high storage
- Use cases:
	- Real-time stream data analytics
	- Generating close captions
#### Accelerated computing instances
- Contain specialized hardware accelerators, like GPUs or FPGAs 
- Use cases:
	- Deep learning
	- Rendering gaming graphics
#### HPC Optimized instances
- Best price performance for running high performance workloads at scale
- Use cases:
	- Weather forecasting
	- Crash simulations
### Creating your EC2 instance
![[creating your ec2 instance.png]]
- When creating your EC2 instance, you'll configure several key components: 
	- The Amazon Machine Image (AMI) is a template that defines the software, such as the operating system, running on your instance. 
	- The key pair is a security credential used to connect to your instance. 
	- The public key stored on the instance and the private key on your local computer. 
	- The Virtual Private Cloud (VPC) is a virtual network dedicated to your AWS account, with one configured by default for each region. 
	- Finally, we have the security group & EBS Volume. The security group acts as a firewall, controlling inbound and outbound traffic, while EBS volume refers to the root storage of the machine image.
### Connecting to your EC2 instance: SSH Client
- Connecting to your EC2 instance is crucial for managing your cloud infrastructure. 
- We'll focus on SSH, Session Manager, and EC2 Instance Connect. 
- SSH is the most common method, requiring a private key for direct terminal access. 
- This approach demands key management and proper security group settings.
### Connecting to your EC2 instance: AWS Session manager
- AWS Session Manager offers secure, keyless access via the Management Console or CLI, eliminating the need for SSH keys or open ports. 
- It’s ideal for security-focused organizations, as it integrates with IAM(Identity and Access Management) for fine-grained control and logs session activity

### Connecting to your EC2 instance: EC2 instance connect
- EC2 Instance Connect provides a browser-based connection without needing an SSH key.
- It’s perfect for quick, temporary access with minimal setup, directly from the AWS Console.
# Load Balancing and Auto-scaling 
- Load balancing ensures even distribution of incoming traffic among multiple EC2 instances, preventing overload on a single server 
	- Ensures high availability
	- Provides horizontal scaling
## Types of load balancers in AWS
![[types of load balancers in AWS.png]]
- Classic Load Balancer
- Network Load Balancer
- Application Load Balancer
- Gateway Load Balancer
## How does load balancing work?
1. Users send requests
![[load balancing 1.png]]
2. Requests hit the load balancer
![[load balancing 2.png]]
3. Primary target group is instantiated by the application load balancer first
![[load balancing 3.png]]
4. If demand increases, the load balancer activates the secondary target group and distributes the load across all instances
![[load balancing 4.png]] 
## What is compute elasticity?
- Elasticity ensures your system can scale up or down based on demand, providing flexibility in resource allocation
- EC2 instances achieve elasticity through EC2 Auto Scaling
## What is EC2 Auto Scaling?
- Auto scaling is an AWS service that automatically adjust the number of active instances based on usage and requirement
- Optimize costs
- Prevent over-provisioning
### How does auto-scaling work?
1. Users send requests
![[auto scaling 1.png]]2. The requests are routed to EC2 Auto Scaling service
![[auto scaling 2.png]]
3. The service then routes requests to the active EC2 instances
![[auto scaling 3.png]]
4. If demand increases, it starts adding new EC2 instances to manage the additional load
![[auto scaling 4.png]]
5. As demand goes down, the newly addedEC2 instances are shut down
![[auto scaling 5.png]]
## Load balancing vs. auto-scaling
| Load balancing                       | Auto-scaling                          |
| ------------------------------------ | ------------------------------------- |
| - Route traffic evenly               | - Ensure demand is always met         |
| - utilize existing EC2 instances     | - Ability to add/remove EC2 instances |
| ![[aws load balancer.png]] | ![[ec2 auto scaling.png]]  |
# Serverless Compute
## EC2 Recap:
- Amazon EC2 is a service that provides compute capacity in the AWS cloud
- Using EC2 gives higher flexibility and control
- Variety of EC2 instance types optimized for different workloads
## Evolving needs: beyond traditional compute
- need for modular, microservices architecture
- Rapid scaling capabilities to meet fluctuating demands
- Automated infrastructure management setup without manual interventions

## Containers and serverless compute
### Containers
- Containers encapsulate applications and their dependencies, in lightweight singular units.
### Why containers?
- Isolate applications from underlying system dependencies
- Share host OS for efficient resource utilization
- Easily movable and portable across environments
### containers in AWS
- Amazon Elastic Container Service. (ECS)
- Amazon Elastic Kubernetes Service.(EKS)
- Easily scale containerized applications up or down.
- integrate with other AWS services.
#### Amazon ECS ( Elastic Container Service)
- Fully managed service for efficient deployment, management, and scaling of containerized applications
- Use cases:
	- Deploying and managing microservices-based applications
	- Plan, schedule, and run batch processing workloads across AWS services
#### Amazon EKS (Elastic Kubernetes Service)
- Container orchestration service specializing in running Kubernetes-powered applications
- Use cases: 
	- Pair with EC2 accelerated computing instances to run ML containers
	- Manage clusters and applications in hybrid cloud environments

In summary, containers are suited for predictable, resource-intensive operations
But what if your application requires compute resources only during specific events or has sporadic heavy workloads?
- AWS addresses these scenarios with **serverless compute.**
### Serverless compute
- Serverless compute focuses on code and outcomes rather than infrastructure, eliminating the need to provision, scale, or maintain servers.
- Event-driven: functions triggered by events in real-time
- Cost-efficient: pay only for actual usage, not pre-allocated resources
#### When to use serverless compute?
- Event driven applications
- Real-time file processing
- Uneven data bursts
- Chatbots and voice assistants
#### Serverless compute in AWS
- AWS Lambda
	- Run code in response to events without provisioning or managing servers
	- Automated compute scaling capabilities
	![[aws lambda.png]]
- AWS Fargate
	- Streamlines application development by providing serverless compute for containers
	- Use cases:
		- Enable AI and ML applications without the need for excessive server provisioning
		- Batch processing of large datasets with parallel compute capabilities
		![[aws fargate.png]]

# Exploring AWS Database Resources
## Introduction to Database as a Service (DBaas)
- Access databases without configuring physical infrastructure or installing software.
	- Relational databases
	- NoSQL databases
	- Memory-based databases
	- Compute-hosted databases (or EC2-hosted databases)
### Relational databases
- structured storage systems organizing data into tables with predefined relationships to other tables using keys.
- why use relational databases?
	- Data integrity
	- Consistency
	- Scalability
- AWS supports relational database management through two services, Amazon RDS and Amazon Aurora.
#### Relational databases in AWS
1. Amazon RDS  (Relational Database Service)
	- RDS offers managed relational databases by controlling setup, operation, and scaling.
	- Key features
		- Wide range of supported database engines
		- Efficient scaling for cloud and on-premises databases
	![[amazon rds.png]]
2. Amazon Aurora
	- Relational database service optimized for MySQL and PostgreSQL engines
	- Key features
		- High performance at approximately one-tenth of the cost
		- In-built continuous backup
		- Automated multi-region replication i.e, multi-region deployments to ensure high availability.
		![[amazon aurora.png]]
### NoSQL databases
- Accommodate diverse data models beyond traditional relational databases, such as JSON and raw documents
- Key features
	- Schema flexibility to deal with evolving data structures
	- Horizontal scalability to handle growing data
- AWS's tow NoSQL database offerings, DynamoDB and DocumentDB.
- Types:
	1. Amazon DynamoDB
		- Serverless architecture, NoSQL, fully managed database with single-digit millisecond performance at any scale
		- Key features
			- High performance with nearly unlimited throughput and storage
			- 99.999% global availability
			- Serverless capabilities for seamless scaling
			![[Amazon DynamoDB.png]]
		- Use cases:
			- is best used for unstructured data like real-time video streaming or media content
			- Tracking inventory or shopping carts based on customer profiles
			- Game platform with player data, session history, and leaderboards
	2. Amazon DocumentDB
		- Fully managed native JSON document database with MongoDB compatibility
		- It can be used for large-scaled document workloads i.e, Operate critical document workloads of any scale with no infrastructure management requirements.
			![[Amazon DocumentDB.png]]
		- when to use DocumentDB?
			- Fast, reliable access to content in your CMS(Content Management systesms) like reviews and images
			- Generate customer recommendations and manage millions of user profiles
			- Unlock GenAI use cases such as semantic search, product recommendations, and chatbots
			![[DocumentDB usecases.png]]
### Memory-based databases
- Designed for high-performance data storage and retrieval, utilizing RAM for faster access
- Optimal use cases
	- Caching frequently accessed data
	- Real-time analytics and data processing
	- High-speed transactional applications
#### MemoryDB for Redis
- AWS's offering for running memory-based databases
- Key features
	- Super-fast read and write capabilities that gives microsecond read and millisecond write capabilities.
	- 99.99% availability
	-  is equipped with fault tolerance to recover instantaneously from any outages or issues that is, Near instantaneous recovery without any data loss
	![[MemoryDB for Redis.png]]
### Compute-hosted or EC2-hosted databases
- Deployed on EC2 instances to simplify data access during compute, following a traditional, manual approach to database hosting
	- Provides granular/Full control over configuration and management
	- Responsibility for backups and patching lies with the user i.e, manual backups and recovery.
	![[Compute databases vs static databases.png]]
# Data Migration Services in AWS
## What is database migration?
- Database migration is moving all of your data from one environment to a brand new environment.
![[Database migration.png]]
## Why do we need data migration?
- Legacy systems unable to meet rapid scalability and efficiency demands
- Generative AI has advanced systemic needs for compute and storage
- Adapt to evolving business needs for scalability and efficiency
- Modernize from legacy systems to meet the demands of contemporary applications
- Facilitate unified data management for adverse sources
## Data Migration in practice
- step one: an assessment of existing data structures, formats, and dependencies of the source data.
- Secondly, preparation of a clear migration plan and organize the source data.
- Third, execution, where necessary tools and operations will be deployed to perform the database migration without inconsistencies.
- validation to verify data integrity post-migration and conduct thorough testing.
- finally, optimization, to fine-tune the performance of applications in the new environment.
![[data migration in practice.png]]
## Migration in AWS
- It offers four services:
	- the Database Migration Service,
	- AWS Snow Family, 
	- DataSync, and 
	- the Schema Conversion Tool
	to enable database migration.
![[migration services in aws.png]]
### AWS Database Migration Service
- Managed service facilitating the movement of 20+ database and analytics engines to AWS
	- Minimizes downtime with automated real-time data replication
	- Supports diverse source and target databases
	- Provides validation checks and task monitoring to ensure data integrity during and post-migration.
	![[AWS Data Migration Service.png]]
### AWS Snow Family
- Offers physical devices to facilitate offline data transfer of petabyte-scale to and from AWS
	- Enables processing data at the edge locations or remote sites that are physically closer to where the source data is stored, for fast large-scale data movement
	- Robust security measures like encryption and tamper-evident seals to ensure data integrity
	![[AWS Snow Family.png]]
### AWS DataSync
- Simplifies, automates, and accelerates **large data transfers** between on-premises storage and AWS Cloud
	- Fast and efficient data transfer through *parallel processing*
	- Seamless integration with S3 and other AWS storage services
	- supports automation through AWS Management Console and internal AWS APIs
	![[AWS Data Sync.png]]
###  AWS Schema Conversion tool
- Facilitates database migrations by automatically converting source database schema to match the target
	- Automates database schema conversion
	- Customization of conversion rules
	- validates the converted schema before performing the migration
	- Diagnostics and recommendations
	![[AWS Schema Conversion Tool.png]]
## When to use which service?
- Database Migration Service is ideal for large-scale, complex data migration projects across heterogeneous databases.
- AWS Snow Family is effective for scenarios with large physical data volumes, restricted bandwidth, or where data must be processed at the edge before moving to AWS.
- AWS DataSync is ideal for scenarios requiring frequent and automated large-scale data transfers between on-premises storage and AWS.
- AWS Schema Conversion Tool is useful for migration projects where the source and target databases have different structures, enabling a seamless transition with reduced manual intervention.
![[data services usecases.png]]
# Network Services
## unlock the power of AWS networking services
- networking resources that enable secure communication and content delivery between users and the cloud through five AWS services - 
	- Amazon VPC,
	- Amazon VPN, 
	- AWS Direct Connect,
	- Amazon Route 53, and
	- Amazon CloudFront.
- building secure and efficient network environment in the cloud
- Designing robust content delivery mechanisms
![[networking services.png]]
## Networking in the cloud
### Amazon Virtual Private Cloud (VPC)
- Amazon VPC establishes networking in AWS by providing a private, logically isolated space in the global AWS infrastructure for defining and launching resources.
- Logically isolated section of the AWS cloud to launch and manage your own resources
- VPCs are regionally hosted, residing in one AWS region.
	![[networking in cloud.png]]
#### Building a logically isolated virtual network
- Amazon VPC provides a dedicated network supporting IPv4 and IPv6 with custom configurable IP address range
- provides Security Layers with: security groups and network access control lists (ACLs)
- offers Complete control over: subnets, route tables and network gateways
#### Understanding key VPC concepts
- Custom configurable IP address range
	- IP addresses are your virtual address spaces on the network, and VPCs let you define it.
	- Your virtual address space in the cloud
	 ![[configurable ip address range.png]]
- Subnets
	- Dividing your VPC IP address range into smaller, manageable segments
		![[subnets.png]]
- Route tables
	- Determines where network traffic from your subnet or gateway is directed
		![[route tables.png]]
- Network gateway
	- Connects your VPC to the internet or other VPCs and controls inbound and outbound traffic.
		![[network gateway.png]]

#### Default vs. Custom Amazon VPC
##### Default Amazon VPC
- Automatic creation with AWS-assigned IP addresses
- Pre-configured settings with a subnet in every availability zone
- can Communicate with the internet by default
![[default amazon vpc.png]]
##### Custom Amazon VPC
- User-defined 
- Customize IP address range, subnets, and route tables
- Require explicit configuration for internet access
	![[custom amazon vpc.png]]

#### Network Security
Security is key for robust networking. AWS offers two services controlling inbound and outbound traffic to VPCs for secure connections.
##### Network Access Control Lists (ACL)
- Virtual Firewall at subnet level
	![[network acl.png]]
##### Network Security Groups (NSGs)
- Firewall for AWS services/instances
	![[network nsgs.png]]

#### VPC endpoints
- Enable private connections between AWS services
- Enhances security by allowing communication between services without public IP addresses
  ![[vpc endpoints.png]]

#### What is AWS PrivateLink?
- AWS PrivateLink is a VPC endpoint enabling Private connectivity between VPCs, supported AWS services, and on-premises networks.
- Benefits
	- Secure data exchange with SaaS applications
	- Simplified network management i.e, reduces network and firewall complexities
	![[aws private link.png]]
### Amazon VPN
- Securely connects your on-premises network to AWS over the internet
- Flexible and accessible, suitable for smaller workloads or temporary connections
  ![[AWS VPN.png]]
### AWS Direct Connect
- Dedicated network connection between your on-premises data center and AWS 
- High bandwidth, low latency, ideal for consistent and mission-critical workloads
-  offers dedicated, highly secure, and internet-free network connections for consistent, high-bandwidth workloads.
  ![[AWS Direct connect.png]]

#### DNS - Internet's address book
- Resolves human-readable domain names to IP addresses used by computers
  ![[DNS.png]]
- Communication between devices on the internet
- Access websites using user-friendly domain names
- DNS, or Domain Name System, acts as the internet's address book, translating user-friendly domain names to IP addresses for website access.
### Amazon Route 53
- Manages domain names and translate them to IP addresses
	- Integration with AWS ecosystem and external services
	- Scalability
	- High availability
	-  It's widely used for hosting web applications and distributing incoming traffic across resources.
	![[Amazon route 53.png]]
	
#### Information movement in the cloud
is challenging due to
- Delay in loading content due to geographical distance
- Limited network capacity impacting content delivery speed
	 ![[information movement in cloud.png]]
#### Content Delivery Networks (CDNs)
AWS solves this problem by providing dedicated content delivery mechanisms.
- Distributed network of servers strategically placed globally to enable fast delivery through caching
- Key characteristics: 
	- Caching for faster content loading 
	- Delivering digital content to end-users over the internet
	- Efficiently handle increased user traffic and demand
	 ![[Content delivery networks.png]]
### Amazon CloudFront
Amazon CloudFront is AWS's global CDN, that excels in fast content delivery across AWS services
- Enhance the speed and security of content delivery to end-users in AWS 
	- Integrates seamlessly with AWS services
	- Accelerates web content, APIs, and streaming
	- Enhances security with DDoS protection and HTTPS support
	 ![[aws cloudfront.png]]
#### How is CloudFront used?
- CloudFront accelerates website content for improved user experience,
- optimizes streaming for reduced buffering times,
- and scales automatically to deliver patches and over-the-air updates to devices.
![[how is cloudfront used.png]]
# Mastering AWS Storage Solutions
-AWS provides a diverse range of storage services tailored to meet various needs
Crucial for securely managing, storing, and retrieving data in the cloud

## Storage types in AWS
1. Object Storage
2. Block Storage
3. File Storage 
4. Cache Storage
![[aws storage services 1.png]]
## What is object storage?
- Storage architecture that manages and organizes data as discrete units called "objects"
- Key characteristics:
	- Horizontal scaling
	- Metadata management
	- Storing unstructured data like large media files, data backups, and data for complex web applications.
### Amazon S3
- A highly scalable and durable object storage service offered by AWS 
- Designed for 99.999999999% (11 9's) durability
- Available in all AWS regions
  ![[aws s3 bucket.png]]
- It's architecture begins with buckets, hosted at the account level. 
- Each bucket contains multiple objects, each comprising data, metadata, and a unique key-value identifier for data access.
#### Storage classes in S3
- S3 storage offers 6 classes based on latency and data requirements:
![[storage classes in s3.png]]
- Standard
	- Durable, scalable, and available in all AWS regions
	- Suitable for **frequently accessed data**
- Intelligent Tiering
	- Automatic **cost optimization**
	- **Moves objects** between tiers **based on changing access patterns**
- One Zone-Infrequent Access (IA)
	- Cost-effective, **single availability zone**
	- Ideal for infrequently accessed data that can be easily reproduced
	- is effective for data not requiring redundancy
- Glacier
	- Low cost, archival storage
	- Long-term archival with *retrieval times ranging from minutes to hours*
- Glacier Deep Archive
	- most economical storage
	- Lowest cost, longest retrieval time
	- Data with minimal access requirements i.e, infrequently accessed data backups.
- S3 Outposts
	- On-premises storage extension
	- Combine private and public cloud data
	-  enabling a hybrid architecture for seamless on-premises and cloud data integration.
## What is block storage?
- Divides data into fixed-sized blocks, each with its unique address
- . Uploaded data is segmented to create a lookup table for block identification during retrieval.
- Use cases
	- Running I/O intensive transactional web applications
	- Right-size big data analytics engines
	- it's commonly used for transactional stores and applications with intensive read-write requirements.
	![[block storage.png]]
### Amazon EBS
- A scalable, high-performance block storage service designed for use with Amazon compute services
- . It comes in HDD and SSD formats, attaches directly to compute services for localized storage, ensuring 99.999% application availability.
	![[amazon ebs.png]]
### Exploring file storage services
- Organizes and stores data in a hierarchical structure
- Key characteristics:
	- Allows multiple concurrent reads and writes across users and services
	- Stores metadata about files for faster retrieval.
		![[file storage services.png]]
## Amazon EFS
- File storage service designed for use with AWS cloud services and on-premises resources
- Use cases:
	- Simplify DevOps i.e used in DevOps for code sharing
	- Enhance content management systems
	- for parallel processing in  data science experimentsAccelerate data science
		![[amazon efs.png]]
## Cache storage services in AWS
- Storing frequently accessed data in a quickly retrievable location
- Accelerates application response times by reducing data retrieval latency
- Minimizes the load on backend servers
	![[cache storage services in aws.png]]
## Amazon ElasticCache
- Caching service that enables seamless, high-speed access to frequently used data
- Use cases: 
	- Store web application session data in-memory
	- Accelerates access to real-time analytics data
	![[amazon elasticcache.png]]
## Revisiting AWS Storage types
![[revisiting storage classes in s3.png]]
## Storage lifecycle policies
- Defines the transition of objects between storage classes in S3, based on predefined rules 
- . These policies govern object transitions between storage classes based on rules
  ![[storage lifecycle in aws.png]]
- Cost and performance optimization
- Improves data management and compliance

## AWS Backup
- Cost-effective, fully managed service that centralizes and automates backup across AWS services ![[aws backup.png]]
- Cross-region backups
- Set retention and deletion policies

# AI & ML services and Machine Learning Process
Artificial intelligence and machine learning are leading the technological world today. Let's look at AWS offerings in this space.
- Artificial intelligence is essentially a systemic way of simulating human intelligence in machines involving tasks like problem solving, speech recognition and learning.
- Machine learning is a subset of AI that focuses on systems that learn from vast amounts of data to infer results.
- AI - mimic human behavior
- ML - Incorporate intelligence learned from data
## AI & ML services
![[ai and ml services.png]]
### AI Services
- AI-focused services in AWS are pre-trained, or auto-trained algorithms that you can directly inherit and use for your applications. 
- They eliminate the need for extensive machine learning implementation knowledge by handling all the logic-building for you. 
#### Amazon Translate 
- Amazon Translate is a service that can automatically translate text into multiple languages. 
	![[amazon translate.png]]
#### Amazon Polly
- Amazon Polly is a text-to-speech service that can convert input text into human-sounding speech.
	![[amazon polly.png]]
	
#### Amazon Lex
- Lex is a managed service that handles the development and deployment of conversational interfaces like chatbots. 
#### Amazon Comprehend
- Comprehend can be used to extract insights like sentiments, entities or identify language from text.
#### Amazon Forecast
- Amazon Forecast is a service that can automatically generate time-series predictions based on input data.
#### Amazon Rekognition
- Amazon Rekognition is an object recognition service that can identify and extract information like sentiments from videos and images.
- Analyze and recognize objects in images
- Perform facial analysis and sentiment detection in videos
![[amazon rekognition.png]]
#### Amazon CodeGuru
- CodeGuru is a developer-friendly service that is used to automate code reviews. It specializes in generating intelligent recommendations for improving code quality.

### ML Services
- enable developers and scientists in building custom ML models.
- tailored for those with ML expertise and specific use cases
#### Amazon SageMaker
- Fully managed service for end-to-end ML lifecycle
- Integrated Jupyter notebooks for model development
- One-click training and deployment
#### Amazon CodeWhisperer
- Automated ML-powered and streamlined code review
- Enhances code quality and identifies issues
	![[amazon codewhisperer.png]]
## ML frameworks
To support the several machine learning and artificial intelligence services, AWS also offers key open-source frameworks to run customizable workflows.
- Open-source frameworks for diverse ML workflows
- Enables robust, scalable, and seamless deployment
- Caters to a wide range of uses
### AWS services enabling ML frameworks
- TensorFlow:
	- TensorFlow is an open-source ML framework developed by Google that can facilitate the development, deployment, and scaling of ML models.
- PyTorch:
	- PyTorch is an ML and deep learning framework built by Meta that can build ML models but specializes in executing computational graph-based systems on-the-fly.
- MxNet:
	- MXNet is an ML framework managed by Apache that specializes in large-scale, distributed training of deep neural networks.

## Sampel ML Pipeline
- The source data that needs to be prepared will be stored in an S3 bucket.
- The ML model development and training will take place in SageMaker which reads data directly from S3.
- For deployment, you package the SageMaker notebook into a container and push it to production through EKS.
- And a lambda job will kick the re-training and deployment of the pipeline whenever new data is available.
![[sample ml pipeline.png]]
# Analytics and BI Services
- Data analytics involves collecting, processing, and transforming data to gain insights. In today’s dynamic environment, it’s an iterative process that supports continuous improvement.
- six key AWS services for data analytics: 
	- Athena, 
	- QuickSight,
	- Kinesis,
	- Redshift,
	- Macie, and 
	- Glue. 
	![[data analytics in aws.png]]
## AWS Athena
- Amazon Athena is a serverless analytics service that enables petabyte-scale data analysis directly from the storage location. 
- It offers data integration across AWS, other clouds, and on-premises sources, with a simple pay-per-query model. 
- Athena also supports SQL-powered machine learning and integrates with QuickSight for data visualization.
![[amazon athena.png]]
## Amazon QuickSight
- Amazon QuickSight is a managed BI service that builds interactive visualizations from various data sources.
- Key features
	- serverless, automatically scales
	- includes generative BI, allowing users to input natural language questions to generate visual answers.
	- It also supports paginated reports for offline sharing.
	![[amazon quicksight.png]]
## Amazon Kinesis
- Kinesis is an AWS service for real-time data stream analysis. It processes data as it flows in, making it ideal for live leaderboards, IoT sensor data, and speeding up traditional batch processing.
- Kinesis is serverless, ensuring efficient scaling with low latencies.
## Amazon Redshift
- Amazon Redshift is an AI-powered data warehousing service with massively parallel processing. 
- It delivers high performance at lower costs,
- supports zero-ETL for unified data integration, and 
- enables secure, parallel project collaboration. 
- Redshift excels in handling large datasets and advanced analytics. ![[amazon redshift.png]]
## Securing data with Amazon Macie
- Amazon Macie is an ML-driven data security service that automatically discovers and protects sensitive data in S3, making it ideal for storing PII.
- It ensures compliance and security,
- and can assess data migration risks before moving data.
## Amazon Glue
- AWS Glue is a data integration service that unifies data across AWS, 
- supporting both batch and streaming data.
- It's ideal for preparing data for advanced analytics tasks like machine learning.
- It’s serverless, scales to petabyte levels,
- and simplifies ETL pipeline development by automatically provisioning and integrating data
## Creating end-to-end data workflow
Imagine analyzing usage data from a mobile app:
-  use Amazon Kinesis to ingest real-time data coming in from the mobile app and store it in S3.
- A function in AWS Glue can then be used to transform the data and move it to Amazon Redshift and Amazon Athena.
- Amazon Macie will be set up across S3, Redshift, and Athena to monitor for any sensitive data being flown into the systems.
- The data in Redshift can be used by a downstream machine learning process for advanced analytics.
- And QuickSight can read data from Athena and build interactive reports to present the analysis to others. ![[creating an end-to-end data workflow.png]]
# Secondary AWS Services Categories
- various secondary services support and enhance the core AWS offerings.
![[secondary aws services.png]]
## Application integration services
- AWS application integrators act like orchestrators, ensuring seamless collaboration among apps. 
- they facilitate communication and coordinate data movement, vital for scalable architectures. We will look at three key services: EventBridge, SQS, and SNS.
	![[application integration services.png]]
### Amazon EventBridge
- Amazon EventBridge responds to events within AWS or externally, connecting with all services to relay occurrences, freeing development from explicit dependencies. 
- It also monitors your AWS environment, tracking integrations for improvement.
	![[amazon eventbridge.png]]
### Amazon Simple Queue Service (SQS)
- Amazon SQS ensures reliable messaging between software components and scales almost infinitely. 
- It is ideal for microservices communication, like dynamic GPS sensor feedback for updating live maps.
- It also efficiently decouples components for seamless background work.
	![[amazon simple queue service.png]]
###  Amazon Simple Notification Service (SNS)
- Amazon SNS is the powerhouse of (application-to-application) A2A and (application-to-person) A2P messaging. 
- It is suitable for sending bulk notifications, SMS to all customers or to other AWS services and 
- operates on a strict order first-in-first-out mechanism that ensures messaging accuracy.
	![[amazon simple notification service.png]]
## Business application services
- Business application services streamline operations, increase efficiency, integrate with AWS services, and support automation.
### Stay connected with customers - Amazon connect
- Amazon Connect is a cloud-based contact center offering easy setup and management. 
- It scales customer support operations during peak times, ensuring efficient support with AI-driven features for personalized interactions and improved customer experiences.
	![[amazon connect.png]]
### Amazon Simple Email Service (SES)
- Amazon SES is a scalable, cost-effective email service for marketing and transactional messages.
- It efficiently sends bulk emails,
- seamlessly integrates for transactional messages like password resets or order confirmations that is, application generated emails, providing reliable delivery and tracking capabilities.![[aws simple email service.png]]
##  Developer services
- AWS offers developer-centric services for streamlined application development. 
- They promote teamwork, integrate with various tools, and enable automated software delivery through continuous integration and deployment.  ![[developer services.png]]
### AWS CodePipeline
- AWS CodePipeline automates delivery pipelines and infrastructure updates, 
- use cases
	- supporting JSON templates for easy pipeline modifications i.e, update existing pipelines or create new ones with JSON templates
	- It can send real-time notifications on pipeline events, and enables the building of end-to-end development workflows.
	 ![[aws code pipeline.png]]
### AWS CodeCommit
- AWS CodeCommit is a fully managed source control service supporting private Git repositories that f*acilitates real-time collaboration* with automated code reviews.
- It can seamlessly integrate with multiple IDEs, CI/CD systems and other AWS tools responsible for deployment of code.
	![[aws code commit.png]]

## Advanced intelligence services
- Advanced intelligence services surpass traditional AI limits, creating smart systems. 
- They connect directly with physical devices using the Internet of Things or perform supercomputer-level computations through quantum computing applications. 
- Let's look at two AWS services that enable advanced intelligence services, AWS IoT Core and Amazon Braket.
	![[advanced intelligent services.png]]

###  AWS IoT Core
- IoT Core securely connects devices to the cloud, simplifying device management by seamlessly linking IoT data to multiple AWS services. 
- It is widely used for predictive maintenance and quality monitoring in industries, and also automates home IoT devices like thermostats and smart TVs.
- Build connected solutions for home automation.
	![[aws iot core.png]]
### Amazon Braket
- Amazon Braket is AWS's quantum computing research solution that provides essential tools and support for managing quantum projects—from code building to running and analyzing.
- It also supports automated testing for quantum applications.
	 ![[amazon braket.png]]