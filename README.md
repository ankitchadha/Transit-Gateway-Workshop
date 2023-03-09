## Prerequisites:
1. You must have key pairs (needed for logging into EC2 instances)
2. Your app account IAM role must have the right permissions to deploy VPCs, subnets, internet gateways, routing tables and EC2 instances
3. Your network-admin account IAM role must have the right permissions to perform CRUD actions on Transit Gateways 
4. The stack deploys public/bastian hosts and opens TCP port 22 from 0.0.0.0/0. SSH will be allowed only with key pair. You can edit the 'PublicSSHLocation' parameter to tighten up the source addresses that are allowed to SSH into the public instances. In case you already have session manager set up, you can delete the section for public instances and use session manager to log into private instances.

## Instructions:
1. From the app account: Deploy TGW-Workshop-App-Account-Ohio template in us-east-2. Select the right key pair. Provide stack name as "app-stack-ohio", and environment name as "app-account-ohio. Make a note of PublicEC2InstanceIP and PrivateEC2InstanceIP from Cloudformation stack outputs. 
2. From the app account: Deploy TGW-Workshop-App-Account-Virginia template in us-east-1. Select the right key pair. Provide stack name as "app-stack-nvirginia", and environment name as "app-account-nvirginia. Make a note of PublicEC2InstanceIP and PrivateEC2InstanceIP from Cloudformation stack outputs
3. From the network-admin account: Deploy TGW-Workshop-Network-Account-Ohio template in us-east-2. Provide stack name as "network-stack-ohio". Make a note of TGWOhioID output
4. From the network-admin account: Deploy TGW-Workshop-Network-Account-Virginia template in us-east-1. Provide stack name as "network-stack-nvirginia". Make a note of TGWNVirginiaID output

## Workshop use cases (after stacks are deployed)
1. Create TGW VPC-attachments in each region. Discuss association vs. propagation
2. Create TGW peering attachment. Discuss and add static routes
3. Can instances ping each other? Why not? Fix Security Groups.
4. Can instances ping each other now? Why not? Fix VPC routing tables.
5. Pause and discuss any other debugging specific use cases. If time permits, discuss VPC Reachability Analyzer for single region or multi region use cases.
6. Create new routing tables in each TGW. Revisit association vs. propagation. Keep VPC-attachments in default routing table, but create propagation into new routing tables
7. Move VPC-attachments from one routing table to another.

## us-east-1 stack output:

PrivateEC2InstanceIP	10.202.20.53
PublicEC2InstanceIP	44.213.242.102
TGWNVirginiaID: tgw-0c78d3474bef9bbe1

## us-east-2 stack output:

PrivateEC2InstanceIP	10.101.20.4
PublicEC2InstanceIP	3.132.15.97
TGWOhioID: tgw-08b37ef428b28d6bc