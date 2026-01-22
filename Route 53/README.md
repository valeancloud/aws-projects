# From Squarespace to AWS: Website & Domain Migration

This project documents how I migrated my small business website (**Harvest Vending Co**) from Squarespace to a fully AWS‑hosted architecture. The goal was to gain more control, improve performance, reduce cost, and integrate tightly with AWS services while keeping the existing domain active.

## What I Built
A complete static website stack on AWS using:

- Amazon S3 for static site hosting  
- Amazon CloudFront for global CDN distribution  
- AWS Certificate Manager (ACM) for HTTPS/SSL  
- Amazon Route 53 for DNS management  
- Visual Studio Code for building the HTML/CSS site  

## Key Steps
1. **Created an S3 bucket** and enabled static website hosting for `www.harvestvendingco.com`.  
2. **Uploaded custom HTML/CSS** and configured a public bucket policy for web access.  
3. **Requested an SSL certificate** in ACM (us-east-1) and validated domain ownership.  
4. **Deployed a CloudFront distribution** using the S3 bucket as the origin and the ACM certificate for HTTPS.  
5. **Created a Route 53 hosted zone** and updated Squarespace nameservers to point to AWS.  
6. **Added DNS records** (CNAME → CloudFront) to route traffic to the new site.  
7. **Tested HTTPS** and verified global propagation.

## Architecture Overview
S3 (Static Website) → CloudFront (CDN + HTTPS) → Route 53 (DNS) → Browser

## What I Learned
- Migrating DNS without transferring a domain  
- How CloudFront handles SSL termination and caching  
- Troubleshooting DNS propagation delays  
- Deploying a static website end‑to‑end on AWS  

## Outcome
The site now loads securely over HTTPS, performs faster globally, and is fully controlled through AWS. This project strengthened my understanding of real‑world DNS, CDN, and static hosting workflows.
