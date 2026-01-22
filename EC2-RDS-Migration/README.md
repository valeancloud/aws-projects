# Data Center to AWS Migration Using EC2 and RDS

This project demonstrates how I migrated an on‑premises workload from a corporate data center to AWS using a Lift & Shift (rehost) strategy. Both the application and its MySQL database were moved to AWS, leveraging Amazon EC2 for compute and Amazon RDS for managed database hosting.

## Project Overview
In this real‑world scenario, I acted as the Cloud Specialist responsible for planning, executing, and validating the full migration. The goal was to move the application stack to AWS with minimal architectural changes while improving reliability, scalability, and operational efficiency.

## Migration Phases
I followed a structured migration approach:

### **1. Planning**
- Sized compute and database requirements  
- Defined prerequisites and resource naming standards  
- Outlined the migration workflow and validation steps  

### **2. Execution**
- Created a custom VPC with public and private subnets  
- Launched an EC2 instance to host the application  
- Provisioned an Amazon RDS MySQL database  
- Configured Internet Gateway and Route Tables for connectivity  
- Ensured best practices for networking and security  

### **3. Go‑Live**
- Performed a dry‑run migration to validate connectivity and performance  
- Executed the final cutover to AWS  
- Verified application functionality and user access  

### **4. Post Go‑Live**
- Monitored application behavior  
- Validated database connections  
- Ensured stable operations after migration  

## Troubleshooting Experience
During testing, I encountered the error:

```
ERROR 2003 (HY000): Can't connect to MySQL server
```

After extensive troubleshooting, I discovered the issue was caused by using the wrong MySQL engine version on RDS. The instance was not running the required **MySQL 5.7.44** version. Once I deleted the incorrect instance and relaunched it with the proper engine version, the connection succeeded.

This experience reinforced the importance of:
- Version compatibility  
- Careful configuration during provisioning  
- Patience and persistence during debugging  

## What I Learned
- Designing VPC networking for real application workloads  
- Deploying EC2 and RDS using AWS best practices  
- Executing Lift & Shift migrations with minimal downtime  
- Troubleshooting database connectivity issues  
- Managing full migration lifecycles from planning to post‑go‑live  

## Outcome
The workload was successfully migrated from the corporate data center to AWS, with the application running on EC2 and the database hosted on RDS. The environment is now more scalable, easier to maintain, and aligned with modern cloud infrastructure standards.
