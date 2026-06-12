# aws-vpc-web-application-project
## project overview
Designed and configured a secure AWS VPC with a public subnet to host a web application
## serviced used
- Amazon VPC
- Public Subnet
- Private Subnet
- Internet Gateway
- Route Tables
- Security Groups
- Amazon EC2
- Apache/Nginx Web Server

## implementation steps
  
### Step 1: Create Custom VPC
- Login to AWS Console.
- Search for VPC.
- Click Create VPC.
#### Configuration:
- Name: Project-VPC
- IPv4 CIDR: 10.0.0.0/16
- Click Create VPC.
### Step 2: Create Public Subnet
- Subnet Name: Public-Subnet
- Availability Zone: ap-south-1a
- CIDR: 10.0.1.0/24
- Create subnet.
### Step 3: Create Private Subnet
- Subnet Name: Private-Subnet
- AZ: ap-south-1b
- CIDR: 10.0.2.0/24
- Create subnet.
### Step 4: Create Internet Gateway
- VPC → Internet Gateways
- Create Internet Gateway
- Name: Project-IGW
- Create and attach to:
- Project-VPC
### Step 5: Create Route Table
- Public Route Table
- Create Route Table:
- Name: Public-RT
#### Add Route:
- Destination: 0.0.0.0/0
- Target: Internet Gateway
#### Associate:
-Public-Subnet
### Step 6: Enable Auto Assign Public IP
- Subnets → Public-Subnet
#### Edit settings:
- Enable Auto Assign Public IPv4

### Step 7: Create Security Group
- VPC → Security Groups
- Name: Web-SG
#### Inbound Rules:
- SSH 22
- HTTP 80
- HTTPS 443
- Source: 0.0.0.0/0
#### Outbound:
-Allow All
### Step 8: Launch EC2 Instance
- EC2 → Launch Instance
- Name:Web-Server
- AMI: Amazon Linux 2023
- Instance Type: t2.micro (Free Tier)
- Network: Project-VPC
- Subnet: Public-Subnet
- Security Group: Web-SG
- Launch.
### Step 9: Connect to EC2
- Using EC2 Instance Connect or SSH.
- ssh -i key.pem ec2-user@public-ip
### Step 10: Install Apache Web Server
- Update packages:sudo dnf update -y
- Install Apache: sudo dnf install httpd -y
- Start service: sudo systemctl start httpd
- Enable on boot: sudo systemctl enable httpd
- Check status: sudo systemctl status httpd
### Step 11: Create Web Page
- cd /var/www/html
- Create page: sudo nano index.html 
### Step 12: Test Website
- Copy EC2 Public IP: paste it on the browser
#### Expected Output:
- AWS VPC-Based Web Application Deployment

