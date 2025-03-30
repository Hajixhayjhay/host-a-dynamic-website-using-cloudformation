# host-a-dynamic-website-using-cloudformation

This project demonstrates how to use AWS CloudFormation to host a dynamic website on AWS. It provisions the necessary resources such as VPC, Auto Scaling Group (ASG), Application Load Balancer (ALB), RDS, NAT Gateway, Route 53, and security groups to ensure that the infrastructure is both secure and scalable.

Overview
This setup uses multiple CloudFormation templates to deploy a fully functional dynamic website hosted on AWS. The resources provisioned include:

VPC with public and private subnets, security groups, and routing.

Auto Scaling Group (ASG) for EC2 instances to run the web application.

Application Load Balancer (ALB) to distribute traffic between EC2 instances.

NAT Gateway to provide internet access to instances in private subnets.

RDS (Relational Database Service) instance for backend database support.

Route 53 for DNS management and domain routing.

Security Groups configured for EC2, ALB, and RDS to ensure secure communication.

Architecture
VPC: A custom VPC is created with public and private subnets across multiple Availability Zones.

Security Groups:

Web Security Group: Allows HTTP (port 80) and HTTPS (port 443) traffic to EC2 instances.

ALB Security Group: Configured to allow inbound HTTP/HTTPS traffic from the internet to the ALB.

DB Security Group: Allows access from EC2 instances to the RDS instance, ensuring that only web servers can communicate with the database.

Application Load Balancer: Distributes incoming HTTP/HTTPS traffic to the EC2 instances behind it.

Auto Scaling Group: Ensures the right number of EC2 instances are running to handle traffic load, scaling up or down as needed.

RDS: Configures a database instance to store dynamic content for the website.

Route 53: Manages DNS settings to point the domain to the ALB.

Prerequisites
Before you can deploy the CloudFormation stack, ensure the following:

AWS Account: You need an active AWS account with the necessary permissions to create the required resources.

AWS CLI: Make sure the AWS CLI is installed and configured for your environment.

IAM Role/Permissions: The user deploying the stack should have permissions to create VPC, EC2, RDS, ALB, and other resources.

Deployment Steps
Step 1: Upload CloudFormation Templates
The following CloudFormation templates need to be uploaded and deployed in the specified order:

vpc.yaml: Provisions the VPC with subnets, security groups, and routing.

nat-gateway.yaml: Configures a NAT Gateway to allow internet access for private instances.

rds-snapshot.yaml: Deploys the RDS instance using a snapshot.

alb.yaml: Configures the Application Load Balancer.

asg.yaml: Creates the Auto Scaling Group with EC2 instances.

route-53.yaml: Configures DNS routing to the ALB.

To deploy each template:

Navigate to AWS Management Console.

Open CloudFormation.

Click Create Stack and choose Upload a template file.

Upload each YAML file in the specified order and follow the prompts to create each resource.

Step 2: Verify Security Group Configuration
The security groups are configured within the vpc.yaml file. After deployment, the following security groups are applied:

Web Security Group:

Allows inbound HTTP (port 80) and HTTPS (port 443) traffic from any source.

Allows outbound internet traffic.

ALB Security Group:

Allows inbound HTTP/HTTPS traffic (ports 80/443) from the internet.

DB Security Group:

Allows inbound traffic from the Web Security Group (EC2 instances) to the RDS database.

Ensure that these security groups are applied correctly to each resource after deployment.

Step 3: Configure Route 53 DNS Records
Once your ALB is up and running, configure your domain in Route 53:

Go to Route 53 in the AWS Console.

Create an A Record (or CNAME) that points to the ALB's DNS name.

Ensure the domain is correctly configured to route traffic to the ALB.

Step 4: Test the Website
After DNS propagation, navigate to your domain. You should see the dynamic website hosted and accessible.

Clean Up
To avoid unnecessary charges, delete the CloudFormation stack after testing:

In the AWS Management Console, navigate to CloudFormation.

Select the stack that was created.

Click Delete to remove all resources associated with the stack.

This will clean up all resources, including VPC, EC2 instances, RDS, ALB, and Route 53 configurations.

Conclusion
This project demonstrates a scalable and secure infrastructure for hosting a dynamic website on AWS using CloudFormation. It integrates multiple AWS services like EC2, RDS, ALB, Route 53, and more, while ensuring security through properly configured security groups.


