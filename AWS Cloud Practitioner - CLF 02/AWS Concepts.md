## AWS Services
- EC2 - Elastic Compute Cloud

## Benefits of AWS
- The cloud has revolutionized business operations by offering scalable, on-demand resources. No longer is there a need for heavy upfront investment in hardware. With AWS, you pay only for what you use, while having the flexibility to scale up or down as needed, with access to a global network of services. This flexibility and cost efficiency are key reasons why millions of customers trust AWS to run their critical applications.
	- Pay for what you use
		- start small and pay only for the resources you use.
		- there are numerous ways to save, such as turning off unused resources, optimizing applications, and using AWS Trusted Advisor to identify cost-saving opportunities.
	- Economies of scale
		-  As AWS expands its global capacity, it can offer lower pay-as-you-go costs due to its vast customer base.
	- Capacity
		- AWS eliminates the guesswork of capacity planning. 
		- Traditionally, businesses had to estimate capacity, often leading to over- or under-provisioning, both of which have costly implications. 
		- With AWS, you can provision resources instantly and scale them in real-time, often within minutes, thanks to AWS's elastic nature.
	- Speed and agility
		- AWS enables rapid environment setup, allowing businesses to experiment with new ideas quickly and affordably. 
		- The lower cost of failure in the cloud encourages innovation and experimentation at a faster pace than on-premise solutions.
	- Save money on datacenters
		- AWS also handles the heavy lifting of infrastructure management, allowing businesses to focus on delivering value to their customers.
	- Go global
		- AWS's global reach allows businesses to quickly deploy applications in multiple regions with just a few clicks. 
		- For example, if they're based in London and their infrastructure is hosted in Europe, but they're expanding operations to the US, you can easily replicate the architecture in a US-based region using tools like AWS CloudFormation — what once took weeks now takes minutes.

## Amazon S3
- Amazon S3 is an object storage service that offers industry-leading scalability, data availability, security, and performance
## Amazon CloudFront
- CloudFront is a content delivery network used to send content like images, videos and more quickly.
- Amazon CloudFront is a fast content delivery network (CDN) service that securely delivers data, videos, applications, and APIs to customers globally with low latency and high transfer speeds.

# Introduction to the AWS Well-Architected Framework
The Well-Architected Framework provides cloud architects with strategies and guidelines for building resilient, scalable, and secure architectures on AWS.
## The six pillars
![[six pillars of well architected framework.png]]
### Security
- Protecting data, systems and assets
- Confidential data through robust identity and access management
- Controls to detect and mitigate security threats
### Cost Optimization
- Avoid unnecessary expenses
- Cost-effective decisions to ensure value on your cloud investment
### Performance Efficiency
- Compute resources used effectively
- Optimal performance to meet demands
- Efficiency as workloads evolve
### Sustainability
- Minimize environmental impact of running cloud
- Aligning your cloud strategy to your corporate environmental goals
### Operational Excellence
- Organize teams around business outcomes and implement observability for actionable insights
- Automate where possible
- Make frequent, small, reversible changes and refine operations procedures frequently
- Anticipate failure and learn from all operational events and metrics
- Use managed services
### Reliability
- Automatically recover from failure
- Test recovery procedures
- Horizontal scaling
- Stop guessing capacity

# Introduction to Cloud Migration
- Migrating to the cloud involves moving your organization’s data, applications, and workloads from on-premises infrastructure to the cloud. 
- Benefits:
	- Significant cost savings
	- Increased flexibility
	- Improved scalability
- While the process may seem daunting, a well-planned approach can help ensure a smooth and successful transition. 
- A key resource for guiding this transition is the AWS Cloud Adoption Framework (AWS CAF). 
- The AWS CAF provides a structured approach to cloud migration, helping organizations design and implement a migration strategy that aligns with their business goals.
## The six perspectives of AWS CAF
![[six perspective of AWS CAF.png]]
- This framework not only reduces migration complexity but also minimizes business risk by providing a clear roadmap.
## Benefits of Cloud Adoption Framework (CAF)
1. Reducing Business Risk:
	- The framework helps you identify potential risks and develop mitigation strategies before migrating.
	- For example, it can prevent common pitfalls like data loss during migration by ensuring proper data backups and transfer protocols. 
	- This proactive approach allows you to address challenges early, helping to maintain business continuity.
2. Improving ESG Performance:
	- Environmental, Social, and Governance (ESG) factors are increasingly crucial for businesses. 
	- The AWS CAF guides you in adopting sustainable practices by:
		- helping you design and implement cloud solutions that optimize resource usage, reduce waste, and lower energy consumption. 
	- For example, it recommends using auto-scaling to ensure that you're only using the resources you need, which directly supports your sustainability goals and reduces your environmental impact.
3. Increasing Revenue and Operational Efficiency: 
	- Migrating to AWS allows your organization to leverage AWS’s vast array of services, enabling faster innovation and quicker responses to market changes. 
	- This agility can lead to increased revenue opportunities. 
	- Additionally, the AWS CAF helps streamline operations by automating processes and optimizing resource management, resulting in greater operational efficiency.
## Common migration strategies
replicating your existing databases to AWS with minimal disruption.
1. AWS Database Migration Service (DMS)
	-  you can migrate databases while keeping them fully operational, ensuring uninterrupted business during the transition.
2. AWS Snowball
	- For large-scale data migrations, AWS Snowball is a popular choice. 
	- Snowball is a physical data transport solution that securely transfers massive amounts of data to AWS. 
	- This method is especially useful when you need to move data quickly and securely, without relying on potentially slow or unreliable internet connections.
![[Alignment with AWS CAF.png]]

# Understand the concepts of cloud economics
## What is cloud economics?
- Refers to the financial considerations of moving to the cloud
- Opportunities to significantly reduce IT expenses compared to traditional IT setups
	- Flexible pricing models
	- Efficient resource usage
	- Elimination of fixed costs
## Fixed vs Variable costs
| Fixed costs                                                                                        | Variable costs          |
| -------------------------------------------------------------------------------------------------- | ----------------------- |
| Hardware                                                                                           | Pay for what you use    |
| Data Centers                                                                                       | scale costs iwth demand |
| Manitenance                                                                                        |                         |
| Paying for full capacity whether it's used or not                                                  |                         |
| Also incur ongoing costs like power, cooling, security, and IT staff for maintenance and upgrades. |                         |
## Bring your own Licenses (BYOL)
- AWS helps you avoid these sunk costs. With AWS, you can Bring Your Own License or opt for included licenses with AWS services. 
- For example, with Bring Your Own License, if you already have a Microsoft Windows Server or SQL Server license, you can apply that existing license to AWS infrastructure. 
- This can be cost-effective because it allows you to leverage your current investments. Alternatively, AWS offers included licenses, where software licensing is bundled with the service, simplifying management and potentially reducing overall costs.
- Avoid sunk costs
- Port existing licenses to AWS infrastructure
- Cost-effective by leveraging current investment
- Alternative: AWS includes licenses bundled into service
## Right-sizing
- Adjust resources to meet actual demand
- can easily resize instances or storage based on usage patterns, ensuring you’re not paying for more capacity than you need.
- Flexibility: significant cost saving and dynamic environment
## Automation
- Automate the setup/management of resources
- Reduces time and effort required to manage infrastructure, minimize human error and ensures consistent configuration
- This not only saves operational costs but also allows your team to focus on higher-value tasks.
## Managed services
- These handle the underlying infrastructure management.
	- Amazon RDS for databases
	- Amazon Lambda for serverless computing
	- Amazon S3 for storage
- This means you don’t need to worry about maintenance, patches, or scaling—AWS handles it for you. Using managed services reduces operational overhead, allowing you to focus more on your core business activities.

# Deploying and operating in AWS
## Provisioning resources in AWS
- allocating and configuring cloud services like servers, storage, and networking—you have multiple approaches.
- You can opt for one-time operations, manually setting up resources, or use automation for consistent, repeatable deployments. 
- AWS offers tools like CloudFormation for Infrastructure as Code (IaC), allowing you to define your cloud environment in templates and automate the process, ensuring consistency and reducing manual errors—ideal for large-scale operations.
## Accessing AWS services
- AWS Management Console
	- AWS Management Console is a web-based user interface that provides a graphical way to manage and configure AWS services, suitable for those who prefer visual management.
- Programmatic Access
	- AWS Command line interface (CLI)
	- Software Development Kits (SDKs)
	- APIs
	- These tools are ideal for automation, integrating AWS services into your workflows, and managing resources programmatically.
- Infrastructure as Code (IaC)
	- means using tools like AWS CloudFormation or third-party solutions like Terraform, you can define your infrastructure as code.
	- This approach is especially useful for automating deployments, ensuring consistency, and managing complex environments. 
 Choosing between these options depends on your requirements. For example, if you need to automate routine tasks or integrate AWS with other tools, programmatic access or IaC might be the best fit. For one-time configurations or monitoring, the AWS Management Console could be more convenient.
## Cloud deployment models
- Public Cloud
	- All resources are hosted on AWS and shared with others
	- Cost efficient and scalable
	- making it suitable for most workloads.
- Private Cloud
	- Dedicated resources to a single organization
	- This is ideal for businesses with strict compliance or security requirements.
- Hybrid Cloud
	- Mix of on-premises and cloud services
	- This model is useful for organizations needing to maintain certain workloads on-premises while taking advantage of cloud scalability and services.
Selecting the appropriate deployment model involves evaluating your organization’s specific needs, including security, compliance, and scalability requirements.

## Connectivity options
- AWS VPN
	- AWS VPN is a secure, encrypted connection between your on-premises network and AWS, leveraging the public internet. 
	- This option is flexible and cost-effective 
	- for smaller workloads or temporary connections.
- AWS Direct Connect
	- offers a dedicated, private network connection from your premises to AWS, 
	- providing lower latency, higher bandwidth, and more consistent performance than internet-based connections.
- Public Internet
	- Public Internet are resources in AWS can also be accessed directly over the public internet, suitable for public-facing applications or services that do not require private network connections.
# Define the AWS Global Architecture
## AWS Geographical diversity
- AWS spans over 30 geographical regions across the globe. Each region is a key part of AWS’s global architecture, much like continents on Earth. With more than 550 points of presence, AWS ensures its services are accessible worldwide. The image on the slide illustrates AWS’s extensive geographical coverage, highlighting its global reach and local presence.
## AWS data centers
- Within each region, AWS operates multiple data centers. 
- These data centers are the core of AWS’s cloud infrastructure. 
- They house the servers, storage devices, and networking equipment that power AWS services, securely managing and processing vast amounts of data. 
- Equipped with redundant power, cooling, and networking, these facilities are designed for high security, reliability, and performance, ensuring continuous operations even in the face of disruptions.
- Think of these data centers as the nerve centers that keep AWS running smoothly around the clock.
## Availability zones
- Each region is further divided into multiple Availability Zones, or AZs. 
- An Availability Zone consists of one or more data centers with independent power, cooling, and networking. 
- These AZs are like self-contained hubs within a region, offering redundancy and high availability. 
- This setup ensures that if one data center experiences an issue, others can seamlessly take over, maintaining service continuity.
## Edge locations: speed of light
- Beyond regions and availability zones, AWS extends its reach to over 400 edge locations globally. 
- Edge Locations are where AWS caches data close to end-users, reducing latency and speeding up access. 
- AWS CloudFront, a content delivery network (CDN) service, uses these Edge Locations to deliver data, videos, and applications quickly and efficiently. 
- These locations act like local delivery hubs, ensuring that content reaches users faster by being stored closer to them, enhancing the overall user experience.

## Black friday: AWs global architecture in action
- Imagine it’s Black Friday, and millions of users are flocking to e-commerce platforms expecting fast, uninterrupted service. 
- During such peak times, AWS’s architecture shows its strength. Data Centers handle the massive processing load, while Availability Zones provide redundancy to ensure uninterrupted service. 
- AWS CloudFront, with its network of Edge Locations, accelerates content delivery by caching it near users, minimizing delays. 
- Together, these components ensure that even during high-traffic events, e-commerce platforms remain robust and responsive.
![[Black friday - AWS global architecture in action.png]]
# Introduction to AWS Compute services
AWS Compute services provide the computing power needed to keep your business running smoothly during such high-demand events like Black Friday.
## Compute: the backbone of digital solutions
- Definition: providing computing power on-demand
- Importance: scalability, flexibility, and cost-efficiency
- AWS offers two primary computing models: **server-based and serverless.**
![[meeting the challenge with AWS.png]]
## AWS EC2
- EC2 is like a sandbox where you can build whatever you want—not just a simple box of sand, but a playground with different zones for various activities.
- You can choose the operating system, storage, and geographic location of your server. With EC2, it's all about customization and control.
![[ec2 unpacked.png]]
## Lambda 
- lambda, on the other hand, is AWS's serverless computing platform. 
- Named after functions from lambda calculus, it's designed to be event-driven, automatically running code in response to various events. 
- For example, it can process a file the moment it’s uploaded or update a database when a record is added. 
- With Lambda, it’s more about convenience than customization.
![[lambda unpacked 1.png]]
![[ec2 and lambda in real life.png]]

- EC2 and Lambda are vast, but AWS also provides services for containerized applications and edge or hybrid computing. 
![[beyond ec2 and lambda.png]]
# Introduction to AWS Database services
- AWS Database services are like sophisticated library management systems, ensuring your data is well-organized and accessible.
- two prominent sections—relational databases and NoSQL databases, each serving different purposes
- RDS is designed for applications needing structured data with clear relationships, like financial systems or e-commerce platforms. 
- NoSQL Databases are more like dynamic magazine racks, offering flexibility and speed in data management.
## Understanding database types
| Relational Databases (RDS)                                              | NoSQL Databases (DynamoDB)                                  |
| ----------------------------------------------------------------------- | ----------------------------------------------------------- |
| Like a well-organized bookshelf                                         | Like a dynamic magazine rack                                |
| supports multiple database engines like MySQL, PostgresSQL, Oracle, etc | flexible schema for unstructured data                       |
| Ideal for traditional applications                                      | Idea for mobile apps, IoT, gaming                           |
| AWS RDS: the sturdy bookshelf of digital world                          | AWS DynamoDB: adaptable and ready for ever-changing content |
| Scalable and cost-effective                                             | Designed for web-scale applications                         |
|                                                                         | Provides single-digit millisecond latency                   |
|                                                                         | DynamoDB uses key-value model                               |
|                                                                         | A key maps to a value                                       |
|                                                                         |                                                             |
- AWS RDS is a fully managed service that simplifies setting up, operating, and scaling relational databases in the cloud.
- Amazon RDS is a managed database service that handles all the infrastructure management, including scaling, backups, and high availability. 
- It’s highly scalable and cost-effective, supporting multiple database engines. This makes it suitable for traditional applications that require complex queries and transactions, like ERP systems, CRM platforms, or financial applications.
- DynamoDB is AWS’s NoSQL database solution, designed for large-scale, high-traffic applications. It offers single-digit millisecond latency, critical for real-time applications.
- DynamoDB’s key-value model is like a wall of safety deposit boxes, where each key unlocks a specific box. This simplicity enables DynamoDB to scale easily and perform consistently, making it ideal for real-time bidding systems, session management, or gaming leaderboards.
## Beyond RDS and DynamoDB
> read more at:
- https://docs.aws.amazon.com/whitepapers/latest/aws-overview/database.html
- Amazon ElastiCache: For caching in-memory data to speed up response times.
- Amazon Neptune: A graph database service for applications navigating complex relationships, like social networks. 
- Amazon DocumentDB: A document-oriented database service, ideal for content management and catalogs.
- Amazon Timestream: A time-series database optimized for storing and analyzing time-stamped data, perfect for IoT and operational applications. 
- Amazon QLDB (Quantum Ledger Database): A ledger database for applications needing an immutable, verifiable transaction log.
![[database-services.png]]
## AWS database migration services
- When migrating existing databases to AWS, AWS Database Migration Service (DMS) plays a crucial role. 
- DMS allows you to migrate databases with minimal downtime, supporting both homogeneous and heterogeneous migrations. 
- Whether moving from on-premises to AWS or between AWS services, DMS simplifies the process, ensuring a smooth transition.
> https://aws.amazon.com/dms/
![[use cases for different databases.png]]
# Introduction to AWS Storage Services
## Storage vs Databases
- Storage plays a critical role in AWS, providing a reliable place to keep your data safe and accessible. 
- Whether you're dealing with backups, large files, or documents, storage ensures that your data is preserved and can be retrieved when needed. This makes it essential for a wide range of tasks, from disaster recovery to archiving. 
- Unlike databases, which are used for organizing and querying structured data, storage is designed to handle large volumes of data without the need for complex management.
- It's about securely storing your data and making sure it's available when you need it, on a large scale.
## Storage services
![[AWS storage services.png]]

### Understanding storage types
| Active/Direct Storage                                                                                                                                                          | Archival Storage                                                                                                                                             |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Like your recent emails, readily accessible                                                                                                                                    | Like old emails, accessed infrequently                                                                                                                       |
| Ideal for day-to-day operations                                                                                                                                                | Ideal for long-term data retention                                                                                                                           |
| **AWS S3:** designed for ease of access and management - Object storage service -  Used for storing and retrieving any amount of data, anytime, from anywhere - Can get pricey | **AWS Glacier:** cost-effective for long-term storage - Used for data archiving and long-term backup - Long-term, low-cost, and secure cloud storage service |
## S3
- stands for **Simple Storage Service**
- is highly scalable, durable, and secure.
- It caters to use cases like website hosting, data backup, and content distribution, designed to maximize benefits of scale and pass those benefits to customers.
### Storage classes
- S3 Standard: 
	- Designed for frequently accessed data, 
	- offering low latency and high throughput, 
	- ideal for content distribution and dynamic websites. 
- S3 Intelligent-Tiering
	- Automatically moves data between frequent and infrequent access tiers based on access patterns,
	- optimizing storage costs. 
- S3 Standard-IA (Infrequent Access): 
	- For less frequently accessed data that still requires rapid access, 
	- cost-effective for backups and disaster recovery. 
- S3 Glacier and S3 Glacier Deep Archive: 
	- These are for long-term archival of rarely accessed data, 
	- offering lower costs while ensuring data security and durability.
![[Other storage services.png]]