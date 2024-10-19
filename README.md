![Alt text](/Host_a_Static_Website_on_AWS (1).png)

---

# Hosting a Static Website on AWS

This repository contains resources, scripts, and architecture diagrams used to deploy a static HTML website on Amazon Web Services (AWS) using EC2 instances. The deployment utilizes several AWS services to ensure high availability, scalability, and security. Below is an overview of the project setup and the resources involved.

## Architecture Overview

The static website is hosted on EC2 instances within a highly available and secure architecture. The deployment makes use of the following AWS services:

1. **Virtual Private Cloud (VPC)**: 
   - Configured with both public and private subnets across two availability zones to enhance system reliability and fault tolerance.

2. **Internet Gateway**:
   - Deployed to allow communication between VPC instances and the internet.

3. **Security Groups**: 
   - Established as a network firewall to control inbound and outbound traffic to the EC2 instances.

4. **Public and Private Subnets**:
   - Public subnets are used for components such as the NAT Gateway and Application Load Balancer.
   - Private subnets house the web servers for enhanced security.

5. **NAT Gateway**:
   - Allows instances in private subnets (Application and Data subnets) to access the internet securely.

6. **EC2 Instances**:
   - Hosted within private subnets for better security and serve the static website content.

7. **Application Load Balancer (ALB)**:
   - Used to distribute incoming web traffic evenly across multiple EC2 instances, improving availability and fault tolerance.

8. **Auto Scaling Group**:
   - Automatically adjusts the number of EC2 instances based on traffic load, ensuring scalability, fault tolerance, and elasticity.

9. **Amazon Route 53**:
   - Used for domain registration and DNS management to direct traffic to the Application Load Balancer.

10. **AWS Certificate Manager**:
   - Secured application communications using SSL/TLS certificates managed by AWS Certificate Manager.

11. **Amazon Simple Notification Service (SNS)**:
   - Configured to send alerts related to Auto Scaling Group activities.

12. **EC2 Instance Connect Endpoint**:
   - Implemented for secure SSH access to EC2 instances in both public and private subnets.

## Deployment Resources

The repository contains the following key resources:

- **Deployment Scripts**: Bash scripts used for setting up EC2 instances, configuring security groups, and deploying the static website.
- **Architecture Diagram**: A visual representation of the system architecture used to deploy the static website.
- **Configuration Files**: Necessary configuration files for setting up the infrastructure.

### Sample Deployment Script for EC2 Instances

The following is an example of a deployment script used to configure an EC2 instance to host the static website:

```bash
#!/bin/bash

# Switch to the root user to gain full administrative privileges
sudo su

# Update all installed packages to their latest versions
yum update -y

# Install Apache HTTP Server
yum install -y httpd

# Change the current working directory to the Apache web root
cd /var/www/html

# Install Git
yum install git -y

# Clone the project GitHub repository to the current directory
git clone https://github.com/inyeza86/Host-Static-Website.git

# Copy all files, including hidden ones, from the cloned repository to the Apache web root
cp -R Host-Static-Website/. /var/www/html/

# Remove the cloned repository directory to clean up unnecessary files
rm -rf Host-Static-Website

# Enable the Apache HTTP Server to start automatically at system boot
systemctl enable httpd 

# Start the Apache HTTP Server to serve web content
systemctl start httpd
```

### Infrastructure Components

- **VPC**: Public and private subnets spanning across two availability zones to ensure high availability.
- **Internet Gateway**: Allows EC2 instances in public subnets to communicate with the internet.
- **Security Groups**: Used as a firewall to manage inbound and outbound traffic.
- **Application Load Balancer**: Distributes web traffic across EC2 instances.
- **Auto Scaling Group**: Manages EC2 instances based on traffic demands.
- **Route 53**: Manages DNS records and domain registration.
- **SNS**: Sends notifications for Auto Scaling events.
- **NAT Gateway**: Provides internet access to EC2 instances in private subnets.

## How to Deploy

1. **Clone this Repository**:
   - Clone the GitHub repository to your local machine or directly to the EC2 instance using Git : https://github.com/inyeza86/Host-Static-Website

2. **Set up the AWS Infrastructure**:
   - Follow the architecture diagram and scripts in this repository to create the required AWS infrastructure, including the VPC, subnets, security groups, EC2 instances, and NAT Gateway.

3. **Deploy the Website**:
   - Use the provided deployment scripts to set up the EC2 instances and deploy the static HTML website.

4. **Configure DNS in Route 53**:
   - Set up DNS records in Amazon Route 53 to point your domain to the Application Load Balancer’s DNS name.

5. **Enable Auto Scaling**:
   - Configure the Auto Scaling Group to automatically manage the number of EC2 instances based on traffic load.

6. **SSL/TLS Certificate**:
   - Use AWS Certificate Manager to secure your website with HTTPS.


## Conclusion
By following the instructions above and using the scripts provided in this repository, you will be able to successfully host a static HTML website on AWS using a highly available, secure, and scalable infrastructure.

---



