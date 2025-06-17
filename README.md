## AWS PROJECT USE IN PRODUCTION

### VPC CREATION
- login to your aws account
- Search for VPC on the AWS console, you will see an option
  for isolated cloud resource VPC, click on that.
- Click on create VPC

![Screenshot 2025-06-17 143057](https://github.com/user-attachments/assets/09b3b0a0-2602-48a2-b72a-4c927f89b743)

  
- select how to create the VPC
  either cearte vpc only or VPC and more
    - if you select vpc only then you will have to create
      everything by yourself
    - if you select vpc and more, then aws will create
      everything for you.
- so select vpc and more
     - aws will create, 
         - private and public subnets in two 
           availability zones (AZ)
         - public and private route tables in two
           AZ
         - internet gateway  

#### More reference = aws plubic private subnet architecture

- Give the project a name
- Configure your CDIR block
- select number of AZ
- select number of public and private subnets          
- Choose the number of AZs in which to create
  NAT gateway
- If you will use s3 bucket in your project then
  select vpc endpoints

- Click on Create VPC  

## AUTO SCALING GROUP CREATION

- Search for auto scaling group on aws console
- Or Unde EC2, you can still find auto scaling group
- Click on auto scaling group
- For best practise, use a launch template to create 
  the auto scaling group, this is because you can use 
  the launch templates across different auto scaling 
  groups.
- Click on launch template to create a launch template.
- Give a name to the launch template
- Enter a description for the template
  (purpose of creating the template)
- Select your AMI
- select your instance type
- Create a key pair
- Under network setting, 
   - don't edit subnet info
   - create a security group
   - Description of SG
   - Select your VPC
   - Add security group rule

- Click on launch template

#### Go back to the auto scaling group console 

- Enter the name of the auto scaling group
- Select the launch template that have created
- Click on the next botton
- Select the VPC that you created
- Select two private subnets
- Click on next
- Click again on next 
- Enter the minimum and maximum number of instance
  that you want to scale with respect to in traffic.
- Click on next
- Click again on next, next
- Click on Create auto scaling group

- Check if your instances are created on aws.

## BASTON HOST CREATION

- launch and instance in the same VPC and enable
  auto assign public IPaddress

- ssh to the baston host 
- Copy your private key to the baston host
- use the key to ssh to your backend servers

- Deploy an application in the backend server
- e.g
   type <w3 schools html basics> on your browser and 
   pickup a basic applicaton code.
   - crate an index.html file and paste the code in it
        - vi index.html
   - Run the code using;
     - python3 -m http.server <port number>
     e.g python3 -m http.server 8000
           
OR
   use the below script to install docker and run prometheus and grafana as a container in the server

      #!/bin/bash
      # Author: Prof Atanga
      # Script requires root access 
      # This script installs docker, prometheus and grafana

      sudo yum update -y
      sudo yum install docker -y
      sudo systemctl start docker
      sudo systemctl enable docker
      sudo docker run --name prometheus -d -p 9090:9090 prom/prometheus
      sudo docker run --name grafana -d -p 3000:3000 grafana/grafana   


## LOAD BALANCER CREATION

- On the aws console, search for EC2 
- scroll down at the left end and search for load balancers
- Click on load balancers
- Select application load balancer
- Provide the load balancer name
- Make sure the load balance is internet facing
- Select the VPC that you created
- Select both AZs and make sure it is in the public subnet
- Create a security group for the load balancer and select it
- Create a target group
   - Right click and open create target group on a new tab
   - Provide the target group name
   - Provide the port on which your application is running
   - Leave everything and click on next
   - select the backend instances
   - Click on include as pending
   - Create target group
- Go back on your load balancer tab, select the target group
  you created.
- Click on Create load balancer 
- Check if access port is open on your load balancer SG
  - if not, open it.

- copy the load balancer DNS and access your application.

**Congratulations, you have successfully set a production
grade environment on AWS with a secured application running on
it**    
