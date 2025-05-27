<h1>AWS Three Tier Web Architecture</h1>

<h2>Description:</h2>

<p>This project is a hands-on walk through of a three-tier web architecture in AWS. We will be manually creating the necessary network, security, app, and database components and configurations in order to run this architecture in an available and scalable manner.</p>

<h2>Audience:</h2>
<p>It is intended for those who have a technical role. The assumption is that you have at least some foundational aws knowledge around VPC, EC2, RDS, S3, ELB and the AWS Console.</p>

<h2>Pre-requisites:</h2>
<p>1. An AWS account. If you don’t have an AWS account, follow the instructions here and click on “Create an AWS Account” button in the top right corner to create one.</p>
<p> 2. IDE or text editor of your choice.</p>

<h2>Architecture Overview</h2>

<h3 align="center" >Amazon 3 Tire Web Application</h3>

![aws 3 tire app](https://github.com/user-attachments/assets/40202626-720f-4b30-927f-d5f62da4e476)

<p>In this architecture, a public-facing Application Load Balancer forwards client traffic to our web tier EC2 instances. The web tier is running Nginx webservers that are configured to serve a React.js website and redirects our API calls to the application tier’s internal facing load balancer. The internal facing load balancer then forwards that traffic to the application tier, which is written in Node.js. The application tier manipulates data in an Aurora MySQL multi-AZ database and returns it to our web tier. Load balancing, health checks and autoscaling groups are created at each layer to maintain the availability of this architecture.</p>

<h2>Setup - Part 0</h2>
<h3>Download Code from Github</h3>
<p>git clone https://github.com/iamtejasmane/aws-three-tier-web-app.git</p>
<h3>S3 Bucket Creation</h3>
<p>1. Navigate to the S3 service in the AWS console and create a new S3 bucket.</p>
<p>2. Select the region you want and give unique name to the bucket.</p>

<h2>IAM EC2 Instance Role Creation</h2>
<p>1. Navigate to the IAM dashboard in the AWS console and create an EC2 role.</p>
<p>2. Select EC2 as the trusted entity.</p>
<p>3. When adding permissions, include the following AWS managed policies. You can search for them and select them. These policies will allow our instances to download our code from S3 and use Systems Manager Session Manager to securely connect to our instances without SSH keys through the AWS console.</p>
   <p>a. AmazonSSMManagedInstanceCore</p>
   <p>b. AmazonS3ReadOnlyAccess</p>
<p>4. Give your role a name, and then click Create Role.</p>

<h3>Networking and Security - Part 1</h3>
<p>Now we will be building out the VPC networking components as well as security groups that will add a layer of protection around our EC2 instances, Aurora databases, and Elastic Load Balancers.</p>
<ul><li>Create an isolated network with the following components:</li>
  <ul><li>VPC</li>
  <li>Subnets</li>
<li>Route Tables</li>
<li>Internet Gateway</li>
<li>NAT gateway</li>
<li>Security Groups</li></ul>


</ul>
