# Refactoring Apps with AWS Managed Services

This project shows how I refactored a **Profile multi tier application** from a basic lift and shift deployment into a **cloud native architecture** using AWS managed services.

## Tech Stack

- **Elastic Beanstalk** → Replaces Tomcat on EC2, handling app deployment, load balancing, and auto scaling.
- **Amazon RDS** → Replaces MySQL on VM/EC2, providing managed relational database service with backups and scaling.
- **Amazon ElastiCache** → Replaces Memcache on EC2 for caching.
- **Amazon MQ** → Replaces RabbitMQ on EC2 for messaging.
- **Amazon Route 53** → DNS management for application endpoints.
- **Amazon CloudFront** → CDN for global content delivery with HTTPS.
- **Amazon S3** → Artifact storage and static content delivery.
- **Amazon CloudWatch** → Monitoring and scaling automation.

## Project Structure

````
/src                                      # Application Source Code
├── Architecture.png                      # Infrastructure Diagram 
├── Guide.pdf                             # Setup to Deploy Stack
├── Prerequisites.md                      # Prerequisites to Deploy Stack
├── README.md                             # This File

````

### **Project Highlights**

This project demonstrates my ability to not just migrate workloads to AWS (Lift & Shift), but to refactor them into managed, cloud-native services — unlocking agility, scalability, and operational efficiency.

### Author
### Anasieze Ikenna - Cloud Engineer

