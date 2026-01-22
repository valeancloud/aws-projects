# Scalable Web Application Using Elastic Beanstalk, DynamoDB, and CloudFront

This project demonstrates how I deployed and scaled a high‑traffic web application using AWS Elastic Beanstalk, DynamoDB, and CloudFront. The application was used during a large global conference with more than **10,000 participants** accessing it simultaneously, both in‑person and online.

## Project Overview
The application needed to handle a sudden spike of thousands of users registering their emails at the same moment for a live raffle. To meet this demand, I designed and deployed a scalable architecture using:

- **Elastic Beanstalk** for application deployment and automatic scaling  
- **DynamoDB** for fast, serverless, highly scalable data storage  
- **CloudFront** for caching static and dynamic content at Edge Locations  
- **Git Bash + SSH** for instance access and troubleshooting  

## Architecture Summary
Elastic Beanstalk (Web App) → DynamoDB (Email Storage) → CloudFront (Edge Caching) → Global Users

This setup ensured low latency, high availability, and the ability to scale seamlessly during peak traffic.

## Key Steps
1. **Deployed the web application** using Elastic Beanstalk with automatic scaling enabled.  
2. **Configured DynamoDB** to store user email submissions with high read/write throughput.  
3. **Integrated CloudFront** to cache content at Edge Locations for global performance.  
4. **Accessed the EC2 instance** via SSH using Git Bash for process validation and debugging.  
5. **Resolved SSH key permission issues** to securely connect to the instance.

## SSH Permission Issue & Fix
When attempting to SSH into the instance, I encountered the error:

```
Permissions 0644 for 'mod4-ssh-key.pem' are too open
```

This occurs when private key permissions are not restrictive enough.  
In UNIX-like systems:

- `6` = read/write (owner)  
- `4` = read-only (group)  
- `4` = read-only (others)  

SSH requires private keys to be accessible **only** by the owner.  
To fix this, I updated the permissions:

```
chmod 400 your_key.pem
```

After applying the correct permissions, SSH access worked as expected and I was able to continue validating the application.

## What I Learned
- Deploying scalable applications with Elastic Beanstalk  
- Designing serverless data storage using DynamoDB  
- Improving global
