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

- **Elastic Beanstalk** → Replaces Tomcat on EC2, handling app deployment, load balancing, and auto scaling.
- **Amazon RDS** → Replaces MySQL on VM/EC2, providing managed relational database service with backups and scaling.
- **Amazon ElastiCache** → Replaces Memcache on EC2 for caching.
- **Amazon MQ** → Replaces RabbitMQ on EC2 for messaging.
- **Amazon Route 53** → DNS management for application endpoints.
- **Amazon CloudFront** → CDN for global content delivery with HTTPS.
- **Amazon S3** → Artifact storage and static content delivery.
- **Amazon CloudWatch** → Monitoring and scaling automation.


### **Project Highlights**

  Demonstrates my ability to:
  
- Migrate real-world workloads to AWS  
- Design scalable, secure cloud architectures  
- Automate provisioning and deployment pipelines  
- Balance performance, cost, and maintainability in production-ready environments


# Author
# Anasieze Ikenna - Cloud Engineer

