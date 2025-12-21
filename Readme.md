# AWS Refactoring Project

This project shows how I refactored a **Profile multi tier application** from a basic lift and shift deployment into a **cloud native architecture** using AWS managed services.

## Project Structure

````
/src                                      # Application Source Code
├── Architecture.png                      # Infrastructure Diagram 
├── Guide.pdf                             # Setup to Deploy Stack
├── Prerequisites.md                      # Prerequisites to Deploy Stack
├── README.md                             # This File

````

## Tech Stack
**Cloud and platform**

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



### **Project Highlights**

  Demonstrates my ability to:
  
- Migrate real-world workloads to AWS  
- Design scalable, secure cloud architectures  
- Automate provisioning and deployment pipelines  
- Balance performance, cost, and maintainability in production-ready environments


# Author
# Anasieze Ikenna - Cloud Engineer

