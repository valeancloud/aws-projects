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

### **4. Post
