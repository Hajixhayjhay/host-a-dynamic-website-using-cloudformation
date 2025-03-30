Project Overview
This project demonstrates how to deploy a dynamic website using AWS CloudFormation. The project utilizes several CloudFormation YAML templates that automate the deployment of necessary AWS resources. These resources include a Virtual Private Cloud (VPC), NAT Gateway, RDS instance restored from a snapshot, Application Load Balancer (ALB), Auto Scaling Group (ASG), and Route 53 for DNS management.

The primary goal is to set up a scalable, secure, and fully-functional environment that serves a dynamic website, complete with a database backend and automatic scaling of the application layer.

Project Structure
The project is organized into the following YAML templates:

vpc.yaml: Defines the VPC, subnets, and related networking resources.

nat-gateway.yaml: Configures the NAT Gateway to allow internet access for private subnets.

rds-snapshot.yaml: Restores an RDS instance from a database snapshot.

alb.yaml: Configures the Application Load Balancer (ALB), including listeners and target groups.

asg.yaml: Creates an Auto Scaling Group (ASG) to automatically scale EC2 instances based on traffic.

route-53.yaml: Configures Route 53 DNS settings for domain name resolution.

Prerequisites

AWS Account: A valid AWS account with sufficient privileges to create resources like EC2, RDS, S3, and CloudFormation.

CloudFormation YAML Files: The YAML files provided (e.g., vpc.yaml, nat-gateway.yaml, rds-snapshot.yaml, alb.yaml, asg.yaml, route-53.yaml).

Domain Name: A registered domain if you want to use Route 53 for DNS (optional).

Sublime Text: Used to edit and manage the CloudFormation YAML files.

How to Use
Step 1: Prepare the CloudFormation Templates
Ensure the CloudFormation templates (vpc.yaml, nat-gateway.yaml, rds-snapshot.yaml, alb.yaml, asg.yaml, route-53.yaml) are correctly set up with the necessary parameters such as instance sizes, VPC settings, and database credentials.

Step 2: Deploy the Stack Using the AWS Management Console
Log in to the AWS Management Console: Navigate to the CloudFormation service.

Create a New Stack:

Click on "Create stack" and choose "With new resources (standard)".

Select "Upload a template file" and choose the appropriate YAML file for each resource (e.g., vpc.yaml, nat-gateway.yaml, etc.).

Follow the prompts to configure stack parameters (e.g., stack name, VPC settings, database credentials, etc.).

Deploy Each Stack in Sequence:

Deploy the vpc.yaml first, followed by the nat-gateway.yaml, rds-snapshot.yaml, alb.yaml, asg.yaml, and route-53.yaml in the order they are listed.

Each stack will take several minutes to complete. You can monitor the stack creation process in the CloudFormation console.

Step 3: Access the Website
Once the stack has been successfully created:

Obtain the Public URL of the ALB: The Application Load Balancer (ALB) will provide a URL for accessing the dynamic website. You can find this URL in the AWS Management Console under the "EC2" service, in the "Load Balancers" section.

Test the Website: Open the URL in your browser to view the dynamic website served through the EC2 instances behind the ALB.

Step 4: Monitor and Manage
Scaling: The Auto Scaling Group (ASG) ensures that the appropriate number of EC2 instances are running based on traffic. Monitor and adjust the scaling settings as necessary in the AWS Management Console.

Logging and Monitoring: CloudWatch monitoring is configured to track application health and performance.

Detailed Steps for Each YAML File
Step 1: VPC and Networking Setup (vpc.yaml)
This template defines:

VPC: Creates a new Virtual Private Cloud (VPC) to isolate the network.

Subnets: Public and private subnets for different resources.

Internet Gateway: An Internet Gateway for internet access from the public subnets.

Route Tables: Defines routing tables for public and private subnets.

Step 2: NAT Gateway Setup (nat-gateway.yaml)
This template configures:

Elastic IP Address: Allocates an Elastic IP for the NAT Gateway.

NAT Gateway: Creates a NAT Gateway in the public subnet to allow internet access for resources in private subnets.

Private Route Table: Defines routing for private subnets to route traffic to the NAT Gateway.

Step 3: RDS Instance from Snapshot (rds-snapshot.yaml)
This template creates:

RDS Instance: Restores a database instance from a snapshot, ensuring that the dynamic website has the necessary database state to operate.

Step 4: ALB Setup (alb.yaml)
This template configures:

Application Load Balancer (ALB): Creates an ALB to distribute incoming web traffic across the EC2 instances.

Listener: Sets up a listener to handle incoming HTTP/HTTPS requests.

Target Group: Defines a target group of EC2 instances that the ALB will route traffic to.

Step 5: Auto Scaling Group (ASG) Setup (asg.yaml)
This template sets up:

Auto Scaling Group (ASG): Automatically scales the number of EC2 instances based on traffic demand.

Launch Configuration: Specifies the instance type and AMI for the EC2 instances.

Scaling Policies: Defines conditions for scaling in and out of instances based on CloudWatch metrics.

Step 6: Route 53 DNS Configuration (route-53.yaml)
This template configures:

Route 53 Hosted Zone: Creates a hosted zone for managing DNS records for your domain.

DNS Record: Sets up an alias record to point your domain to the ALB's DNS name, allowing users to access your website using the custom domain.

Cleanup
To delete the resources created by CloudFormation, go to the CloudFormation Console, select each stack, and choose Delete Stack. This will remove all resources and prevent ongoing charges.

Troubleshooting
Stack creation fails: Check the AWS CloudFormation events and logs to identify issues with resource creation. Issues are often related to IAM permissions or incorrect parameters in the template.

Access issues: Ensure that your security groups and network ACLs are correctly configured to allow inbound traffic to the EC2 instances or Load Balancer.


Acknowledgments
AWS CloudFormation documentation and resources: https://aws.amazon.com/cloudformation/

AWS EC2, RDS, ALB, and ASG service documentation.

