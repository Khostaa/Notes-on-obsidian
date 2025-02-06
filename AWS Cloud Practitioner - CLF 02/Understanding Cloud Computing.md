- Cloud computing is the delivery of technology services including compute, storage, databases, networking, software, and more - over the internet with pay-as-you-go pricing.
- Instead of owning your own computing infrastructure or data centers, you can rent access to these services from providers like Amazon AWS, Microsoft Azure, Oracle, or Google Cloud Platform
## Why Cloud Computing?
- Increased traffic can lead to problems if the infrastructure can't keep up, causing slowdowns.
- When traffic increases, you'll need to buy or rent more servers to handle the demand
- This is costly and time-consuming. Even if the servers are only needed temporarily, you'll still pay for them year-round.
- Alternatively, you can use cloud computing. You can host your website on a cloud server, accessible remotely just like a dedicated server.
- As traffic increases, you can instantly scale up computing power in the cloud on-demand.
- When traffic decreases, you can release those resources back to the cloud.
- Billing works like utilities — pay for what you use.

## Cloud Computing vs on-premise
- Cloud computing is more scalable and offers faster setup compared to on-premise servers.
- However, the best approach depends on your specific needs. However, on-premise servers can be cheaper or more secure in some cases.
- ![[Cloud Computing vs on-premise.png]]
> You can do more with the cloud than host a website on a server. You could store, back up, and recover data, create cloud-native applications, stream audio and video, deliver software on demand, analyze data, embed artificial intelligence models, and much more.

# The Power of Cloud
Cloud providers offer many services.
## Cloud Computing Characteristics
### virtualization
- Fundamental technology that powers cloud computing.
- Virtualization powers cloud computing by splitting a physical server into several virtual servers, each with its own operating system.
- This efficient use of resources makes the virtualized machine more portable and manageable, reducing the need for physical machines and maximizing server output. This allows cloud providers to operate on economies of scale.
### scalability
- Easily add and remove resources as you need them.
- For instance, an e-commerce site can handle increased traffic during peak times, like Black Friday, by scaling up resources.
#### Types of scaling
- Vertical
	- Vertical scaling changes the power of an existing instance
- Horizontal
	-  horizontal scaling increases the number of instances, sharing the workload across multiple devices.
![[types of scaling.png]]
### cost
- Only pay for resources when you are using them
	- Pay-as-you-go
	- No capital expenses of
		- buying hardware and software
		- managing onsite infrastructure.
- However, for clear and stable resource needs, an on-premise solution might be more cost-efficient in the long term. The best solution depends on the use case.
### speed
- The cloud makes resources available to you almost immediately when you ask for them. This is called on-demand resourcing. 
- There is a fast set-up time 
- and you can deploy technology services in a matter of minutes. 
- No waiting around for hardware to be ordered, installed, cabled, and configured before using it.
### performance
- Access to fast and efficient computing resources
- Cloud give access to
	- Worldwide network of data centers
	- fast and efficient computing hardware
### growth
- Grow using a wide range of resources and services
	- on-demand resourcing limits growth constraints
	- Additionally, you can expand to new geographic regions and deploy globally in minutes.
	- provision resources across a global network
### reliability
- Cloud computing ensures the durability and availability of data and services by replicating data at multiple redundant data centers. 
- If one data center is impacted by a disaster, data remains available elsewhere.
### security
- Secure storage and management of your data
	- external party responsible for security
	- Particularly risky for businesses in highly regulated sectors
	- Cloud is becoming more and more secure.
# Cloud service models
- Infrastructure as a Service (IaaS)
	- offers cloud infrastructure
- Platform as a Service (PaaS)
	- offers infrastructure and software for application development
- Software as a Service (SaaS)
	- offers ready-to-use applications in the cloud
![[Cloud service models.png]]

- For each feature, select the lowest-tier service model where the cloud provider manages that feature.
![[feature managed.png]]
## The cloud pyramid
![[cloud pyramid.png]]
- As we move up, abstraction increases and control decreases.
- More abstraction means less detail but easier management. 
- The highest level of abstraction covers the entire system, while lower levels involve fewer components.
## Other cloud service models
- Function as a Service (IaaS)
	- FaaS is a variation of SaaS focused on single functions, like identity authentication or payment transactions. 
	- FaaS uses a "serverless" billing model, meaning you pay for the service rather than renting servers.
- Hardware as a Service (HaaS)
- Database as a Service (DBaaS)
- Disaster Recovery as a Service (DRaaS)
- Network as a Service (NaaS)
- This phenomenon is called **XaaS, or Anything as a Service**, coverling all cloud services available over the internet.
# Cloud deployment models
-  Choosing a cloud deployment model is one of the first choices to make when migrating to the cloud.
- It's informed by how much control you need over your cloud environment, which is defined by your business requirements and budget.
## Private Cloud
- is private by design and designated for exclusive use by its tenants.
- This means to access a private cloud, you need to connect to a network link, which means special network access needs to be set up by IT.
- An organization may hire a third party to host their private cloud infrastructure or host it themselves.
- This gives an organization direct control over the resources available, alongside with how data is stored.
- For example, you can specify what kind of operating system and the exact hardware you want. This is flexibility that does not come with other models.
- Pros: Direct control of resources and data
- Cons: More upfront investment
- Private cloud can also be located off-premises.
## Public Cloud
- The cloud infrastructure is shared and open for use by the general public. 
- The infrastructure is owned and managed by a cloud service provider, like AWS or Azure. 
- Public clouds are Internet accessible. This lets organizations get started quickly with minimal investment.
- This lets organizations get started quickly with minimal investment. They don't have to host or commit to an infrastructure, instead they can pick what services they need from a provider.
-  They can also instantly buy more capacity making it easier to scale.
- If it's important to have direct access to the data centers or hardware than public cloud is not a good choice.
- Public cloud providers keep their data center locations secret, even to their clients, for security reasons.
## Hybrid Cloud
- This is when an organization uses a combination of two or more distinct models. The different models interact with each other via a network link and can share data and services.
- It's more of a question of where data and services are physically stored.
- For example, you could store sensitive patient data on a private cloud for security reasons and use an application on the public cloud, like a business intelligence tool, to process it. 
- Hybrid clouds are useful in the case of cloud bursting. This is when a private cloud is overwhelmed by demand and hits capacity. To avoid disruption of service to users, traffic is moved to a public cloud instance.
- A classic example of this are seasonal spikes. For example, retail businesses can expect extraordinary traffic during sales periods like Black Friday or Boxing Day. This allows organizations to cost-effectively handle periodic spikes with pay-per-use pricing.
## Other deployment models
### Multi cloud
- Multicloud combines different cloud provider services. 
- For example, an organization could use Azure for backups, AWS for website hosting, and Google Cloud for analytics. 
- Multicloud provides flexibility on choosing pricing plans and service offerings. 
- It also reduces reliances on one vendor.
- Don't confuse this with the hybrid model which uses a combination of cloud deployment model, not services!
### Community
- This is when the cloud's infrastructure is shared by a specific community for their exclusive use. 
- Usually this community has a shared interest or concern, whether it be having the same security requirements or jurisdiction, or sharing a mission. 
- This shared infrastructure allows for easier collaboration and sharing of data, whether it's research data between institutions or government data across agencies. 
- The infrastructure itself can be managed and hosted internally or externally.

# Regulations on the Cloud
- Having servers spread out across the globes reduces latency. The greater the distance between two points, the longer it will take for data to get there. This delay between the moment data is transmitted and the moment it is received is known as latency. 
## General Data Protection Regulation (GDPR)
- An example of data privacy law is the European Union's General Data Protection Regulation, or GDPR
-  it regulates how personal data is collected, processed, and stored from users in the European Union.
- For example, before a company collects any data, they need to explicitly get consent. 
- Companies also need to notify users of any data breaches in a timely manner. 
- Personally identifiable information must be encrypted, anonymized, and/or pseudonymized when stored depending on scenario. 
- And, some regulations affect how data can be physically moved, for example, personal data can't leave EU borders unless the company can guarantee that the data will have the same level of protection wherever it may land outside the EU. 
- Can you see how this affects cloud computing where data can move to different servers around the world? There's major incentive to comply to GDPR. 
- The fine can be up to 20 million euros or 4% of the company's worldwide annual revenue - whichever is greater.
### What is personal data?
- A lot of these regulations talk about "Personal Data". What does that exactly mean? 
- The European Commission defines it as any information that relates to an identified or identifiable living individual. 
- Different pieces of information, which collected together can lead to the identification of a particular person, also constitute personal data. 
- This includes home address, first name, last name, email address, location data, IP address, racial or ethnic origin, political opinions, sexual orientation, and health related data. 
- Some of these on their own may not identify a specific individual, but for example, if you combine all the location data of a given person, it can get much easier to identify who they are by where they spend the most time, like their home address. Personal data is often referred to as PII, which stands for personally identifiable information.
![[data protection regulation across globe.png]]
# Cloud Computing roles
## familiar data roles and the cloud
- Data scientist
	- Run computationally expensive analyses on the cloud
- Machine learning scientist
	- Train and deploy machine learning models on the cloud
- Data engineer
	- Build pipelines on the cloud to ingest, transform, and store big data
- Data analyst
	- Access data on the cloud via business intelligence tools
## Creation of new cloud roles
### Cloud architect
- Solutions architect for the cloud
- Design cloud infrastructure for a given business problem
- Plan the deployment of the infrastructure
- Ensure scalability and optimized for cost
### Cloud engineer
- Build, maintain and monitor cloud services
- Migrating operations to the cloud
### DevOps engineer
- Software Development + IT Operations
- Infrastructure as code
- Ensure the reliability, availability, and scalability of the cloud through software development and automation
### Security engineer
- Spec security requirements
- Test and assess security of data on the cloud
- Responsible for protecting organization and  user data

# An overview of providers
  ![[Market shares of Cloud providers as of 2023.png]]
## The rise of cloud computing
- Cloud computing services vital for modern companies
- IaaS and PaaS offer significant benefits
- Enable agility, efficiency, innovation
- Reduce costs, focus on core business

## Making a choice
- Best cloud provider meets company needs
- Leverage cloud specialists' knowledge.
- Contact providers directly
- Consider current infrastructure and datacenter costs
- Evaluate costs for managing hardware andstorage
- Assess costs for app depreciation, migration, or rebuild for cloud
- Consider hiring cloud specialists, benefits to company and customers, and potentialcloud migration risks

## Amazon Web Services (AWS)
- Launched in 2006 (Google Cloud in 2008, Microsoft Azure in 2010)
- Breadth of services:
	- Computing
	- Storage
	- Analytics
	- Security and enterprise applications
	- Machine learning
### AWS Professional  cloud services
 - AWS Simple Storage Service (S3)
 - AWS Elastic Compute Cloud (EC2)
 - AWS Relational Database Service (RDS)
![[AWS professional cloud services.png]]
### AWS Professional data services
- AWS Redshift (analytics - data warehousing)
- AWS Kinesis (real time data movement and analytics)
- AWS SageMaker (predictive analytics and machine learning)
![[professional data services.png]]
### AWS case study
#### Nerd Wallet
NerdWallet helps customers make financial decisions, using data science and machine learning to provide personalized financial recommendations. NerdWallet wanted to optimize deployment cost and time: it was taking too long to go from concept to launching into production.
![[case study part I.png]]
Improvements:
- Launching models now takes days instead of months, and data scientists can focus more on strategy and other projects.
![[case study part II.png]]
>  Find more case studies here:
 - https://aws.amazon.com/solutions/case-studies/

## Microsoft Azure
- Microsoft first started by re-purposing some of its software, such as Microsoft Office, Windows Server, or SQL Server, to the cloud, and there is a tight integration between these and Azure services.
### Azure cloud services
Some key services: 
1. Azure Blob Storage: for file storage
2. Azure Virtual Machine: for Computation
3. Azure SQL Database: for databases
### Microsoft fabric
- It is a software as a service that brings together different Microsoft solutions for enterprise use. 
- It covers everything from data movement to data science, real-time analytics, and business intelligence, and 
- it will be a key service offering for Microsoft.

### Azure data services
- **Data Lake Storage** (store data before cleaning)
- **Stream Analytics** (real-time analytics)
- **Machine Learning** (train and deploy machine learning models)
### Azure case study
![[azure case study part I.png]]
![[azure  case study part II.png]]
> Find more case studies at:
-  https://customers.microsoft.com

## Google Cloud
- Google Cloud acknowledges that multi-cloud - a combination of different cloud provider services - is the future and that consumers don't want to be locked in.
- launched **Google Cloud Anthos**, a service that allows customers to manage and deploy workloads across clouds without worrying about the different environments and APIs. In other words, Anthos lets you deploy and run hybrid multi-cloud solutions, combining on-premise servers and several cloud providers all in one place.
### Google Cloud Services
- Google Cloud Storage: for file storage
- Google Cloud Compute: for computation tasks
- Google Cloud SQL: for database task
![[Google Cloud services.png]]
### Google Cloud data services
- Big Query (data warehouse)
- Dataflow (batch and stream data processing)
- AutoML (machine learning model training and development)

### Google Cloud case study
![[google cloud case study I.png]]
![[google cloud case study II.png]]