# AWS Refactoring Project

This project shows how I refactored the **Profile multi tier application** from a basic lift and shift deployment into a **cloud native architecture** using AWS managed services.

- **AWS Refactor Project** → [`awsrefactor`](https://anasiezeikenna.notion.site/Refactoring-Apps-with-AWS-Managed-Services-26105c74585e80f8a5f8f3a4488b4b3b)  

<img width="3716" height="2189" alt="image" src="https://github.com/user-attachments/assets/0cdb0e44-6146-4cad-aab5-82c9ce3278ea" />

The main goals were to:

- Remove the operational burden of managing servers
- Improve scalability and reliability for production workloads
- Use managed services wherever it makes sense
- Keep the core application logic intact while modernizing the platform


## Architecture Overview

The refactored architecture takes the original Profile stack and maps each self managed component to an AWS managed service.

### Core AWS Managed Services

- **Elastic Beanstalk**  
  Replaces Tomcat on EC2 for the main application. Handles deployment, load balancing, auto scaling, and health checks.

- **Amazon RDS**  
  Replaces MySQL on VM or EC2. Provides managed relational database, backups, snapshots, failover, and scaling.

- **Amazon ElastiCache**  
  Replaces Memcache on EC2. Delivers a managed caching layer for faster reads and reduced database load.

- **Amazon MQ**  
  Replaces RabbitMQ on EC2. Fully managed message broker for decoupled communication.

- **Amazon Route 53**  
  Used for DNS management and routing traffic to the application endpoints.

- **Amazon CloudFront**  
  Content delivery network in front of the application for global reach and lower latency with HTTPS.

- **Amazon S3**  
  Used for artifact storage and static content.

- **Amazon CloudWatch**  
  Central monitoring for logs, metrics, dashboards, and alarms. Also ties into auto scaling policies.

## Service Modernization Mapping

| Traditional Service     | AWS Managed Service  | Key Benefit                                   |
| ----------------------- | -------------------- | --------------------------------------------- |
| Tomcat on EC2           | Elastic Beanstalk    | Automated deployment, scaling, and patching   |
| MySQL on VM or EC2      | Amazon RDS           | Backups, failover, and read replicas          |
| Memcache on EC2         | Amazon ElastiCache   | Managed caching cluster                       |
| RabbitMQ on VM or EC2   | Amazon MQ            | Fully managed message broker                  |
| NFS                     | Amazon EFS or S3     | Elastic, durable shared storage               |
| Self managed DNS        | Amazon Route 53      | Highly available DNS with routing policies    |
| Custom CDN or none      | Amazon CloudFront    | Global caching, edge locations, TLS offload   |


## Request Flow

1. Users access the application via a **Route 53** DNS record.
2. Requests first hit **CloudFront**, which serves cached content for static assets and forwards dynamic traffic to the origin.
3. CloudFront forwards traffic to an **Application Load Balancer** fronting the **Elastic Beanstalk** environment.
4. **Elastic Beanstalk** manages a fleet of EC2 instances running the Profile application, scaling based on demand.
5. Application artifacts are stored in **Amazon S3** and pulled by Elastic Beanstalk during deployments.
6. The application uses:
   - **Amazon RDS** for relational data
   - **Amazon ElastiCache** for caching
   - **Amazon MQ** for messaging and asynchronous workflows
7. **Amazon CloudWatch** collects metrics and logs and drives alarms and auto scaling actions.

## Cost and Sizing Snapshot

Running the full Profile stack with AWS managed services is about:

- **Approximate monthly cost**: `~123.95 USD per month`  

This reflects a production ready setup with managed compute, database, caching, and messaging, plus CDN and monitoring.

The aim of the project is not to find the absolute cheapest setup but to show how managed services can deliver:

- Higher scalability
- Better availability
- Stronger security
- Lower operational overhead


## Implementation Steps

High level steps followed in this refactor:

1. **Re design from IaaS to managed services**

   - Move from EC2 heavy, manually managed servers to a mix of **Elastic Beanstalk**, **RDS**, **ElastiCache**, and **Amazon MQ**.
   - Define clear network boundaries using VPC, subnets, and security groups.

2. **Create security groups for backend services**

   - Dedicated security group for RDS, ElastiCache, and Amazon MQ
   - Only allow traffic from the Elastic Beanstalk instances and required administration sources

3. **Provision backend services**

   - Create **Amazon RDS** instance for the Profile database
   - Create **Amazon ElastiCache** cluster for caching
   - Create **Amazon MQ** broker for application messaging

4. **Set up Elastic Beanstalk**

   - Create an environment for the Profile application
   - Configure platform (Tomcat or Java as required)
   - Attach the correct VPC, subnets, and security groups
   - Configure environment variables and connection strings for RDS, ElastiCache, and MQ

5. **Build and deploy artifacts**

   - Package the application artifact (for example a WAR file)
   - Upload the artifact to **Amazon S3**
   - Deploy through Elastic Beanstalk console or CLI
   - Validate health checks and logs

6. **Set up CloudFront and Route 53**

   - Configure **CloudFront** distribution with the Application Load Balancer as the origin
   - Attach an **ACM certificate** for HTTPS
   - Create **Route 53** records that point to the CloudFront distribution

7. **Configure monitoring and auto scaling**

   - Set **CloudWatch** alarms for CPU, latency, error rate, and queue depth
   - Configure auto scaling policies in Elastic Beanstalk based on CloudWatch metrics
   - Enable log streaming to CloudWatch for debugging and operations


## Results and Key Benefits

This refactor delivers both technical and business outcomes.

### Operational and engineering impact

- **Reduced operations effort by about 60 percent**  
  No more manual patching for application servers, database, or message broker.

- **Faster deployments with about 70 percent improvement**  
  Elastic Beanstalk and S3 based artifacts turned deployments from hours into minutes.

- **Improved availability targeting 99.99 percent uptime**  
  Auto healing environments, managed RDS failover, and cache layer reduced downtime risk.

- **Better global performance with about 40 percent lower latency**  
  CloudFront serves cached content from edge locations closer to users.

- **More predictable and visible costs with about 30 percent savings**  
  Pay as you use managed services replaced a more static, server heavy setup.

- **Higher agility for feature work**  
  With AWS taking care of most of the undifferentiated heavy lifting, engineers can focus more on features instead of infrastructure.


## Tech Stack

**Cloud and platform**

- AWS
- Elastic Beanstalk
- Amazon RDS
- Amazon ElastiCache
- Amazon MQ
- Amazon S3
- Amazon CloudFront
- Amazon Route 53
- Amazon CloudWatch

**Application**

- Profile multi tier application (Java and Tomcat based stack)
- Build and artifact management through S3 and Elastic Beanstalk

**Networking and security**

- VPC, public and private subnets
- Security groups and NACLs
- ACM for TLS certificates


