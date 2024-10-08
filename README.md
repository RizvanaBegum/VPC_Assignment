 Secure Cloud Infrastructure Setup with VPC Peering README

## Overview
This README provides a guide to setting up a secure and scalable cloud environment for deploying applications and resources. The infrastructure includes hosting public-facing web servers, a private database, and an application server with internet access. Additionally, it enables access to a private database hosted in another region via VPC peering.

## Scenario:

As an IT infrastructure manager, you have been tasked to provide a secure and scalable cloud environment for deploying applications and resources. The requirement is to host web servers that should be accessed by public and to host a database with no access to public and an application server which is maintained privately but needs internet access to get updated and for other necessary communications. Additionally, the company needs to access the database which is hosted privately in VPC of other region.

# Solution:


## VPC Design
- Created a Virtual Private Cloud (VPC) with public and private subnets using CIDR block segmentation.
- Allocated appropriate subnets for public and private resources.

## Public-Facing Web Servers
- Deployed web servers (e.g., EC2 instances) within the public subnet.
- Connected the public subnet to an Internet Gateway to make the servers accessible from the internet.
- Configured security groups to allow inbound traffic.

## Private Database
- Placed the database within the private subnet.
- Ensured no internet gateway is attached to the subnet to prevent direct internet access.
- Allowed necessary inbound traffic only from the application server's subnet (via security group rules) and outbound traffic as required.

## Application Server
- Hosted the application server (e.g., EC2 instance) in another private subnet.
- Connected to a NAT Gateway to allow outbound internet access for fetching updates and communicating with external services.

## VPC Peering for Database Access
- Established VPC peering between the VPC containing the web server and the VPC in the other region.
- Configured route tables and security group rules to allow secure communication between the peered VPCs.

## Network Access Control
- Utilized network access control lists (NACLs) to control traffic flow at the subnet level if necessary, providing an additional layer of security.

## Internet Gateway and NAT Gateway
- Attached an internet gateway to the VPC to enable internet access for resources in the public subnet.
- Used a NAT gateway in the public subnet to allow resources in the private subnet to initiate outbound connections to the internet while remaining private.

## Routing
- Configured route tables for each subnet to direct traffic appropriately, ensuring that traffic destined for the internet uses the internet gateway in the public subnet, while internal traffic uses local routing within the VPC.

By implementing these VPC concepts effectively, a secure and isolated environment for cloud resources has been created, meeting the requirements of hosting public-facing web servers, a private database, and an application server with internet access, while also enabling access to a private database in another region via VPC peering.
