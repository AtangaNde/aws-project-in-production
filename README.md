## AWS PROJECT USE IN PRODUCTION

### Project Architechture

![image](https://github.com/user-attachments/assets/3baeb7b7-1482-42b0-abc6-3fef100cd0e9)


### VPC CREATION
- login to your aws account
- Search for VPC on the AWS console, you will see an option
  for isolated cloud resource VPC, click on that.

![Screenshot 2025-06-17 143057](https://github.com/user-attachments/assets/09b3b0a0-2602-48a2-b72a-4c927f89b743)

- Click on create VPC
- select how to create the VPC
  either cearte vpc only or VPC and more
    - if you select vpc only then you will have to create
      everything by yourself
    - if you select vpc and more, then aws will create
      everything for you.
- so select vpc and more

![Screenshot 2025-06-17 144555](https://github.com/user-attachments/assets/98a87188-6266-4d36-901e-108c16a8e744)

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

  ![Screenshot 2025-06-17 145246](https://github.com/user-attachments/assets/b95947b1-8169-427e-9442-505f26ca7c3c)
  ![Screenshot 2025-06-17 145613](https://github.com/user-attachments/assets/850e01f5-29e9-4faa-87c3-cc3c780712af)
  ![Screenshot 2025-06-17 145521](https://github.com/user-attachments/assets/b86109f0-b8f0-4330-8747-58806ef96799)




## AUTO SCALING GROUP CREATION

- Search for EC2, scroll down at the left end
- Click on auto scaling group
- Click on Create auto scaling group
- For best practise, use a launch template to create 
  the auto scaling group, this is because you can use 
  the launch templates across different auto scaling 
  groups.

![Screenshot 2025-06-17 150733](https://github.com/user-attachments/assets/2ab1d918-4643-41d0-abe5-b3dddfdfccfc)

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

![image](https://github.com/user-attachments/assets/ea3ca540-f20c-4a25-b467-0ce1dd727fea)
  

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

![Screenshot 2025-06-17 154806](https://github.com/user-attachments/assets/3a3f3186-32c2-4830-b067-f26fc5e4f759)
  
- Check if your instances are created on aws.

 ![Screenshot 2025-06-17 155021](https://github.com/user-attachments/assets/ecef4b9e-993d-4846-baa3-f0b5593aa52e)

## BASTON HOST CREATION

- launch and instance in the same VPC and enable
  auto assign public IPaddress

![Screenshot 2025-06-17 155745](https://github.com/user-attachments/assets/b3c6f088-5753-4c67-9e81-4607a85285a0)

- ssh to the baston host

  ![Screenshot 2025-06-17 160405](https://github.com/user-attachments/assets/fdb2d16a-f7dd-4ea4-b4b6-cdf60d38a084)

- Copy your private key to the baston host
- 
           scp -i awskey.pem /c/Users/USER/Downloads/awskey.pem ec2-user@54.179.167.114:/home/ec2-user

![Screenshot 2025-06-17 160924](https://github.com/user-attachments/assets/d83619fe-62c8-49ef-a3e5-6e98f33a828d)

- use the key to ssh to your backend servers using the private IPaddress

![Screenshot 2025-06-17 164222](https://github.com/user-attachments/assets/3cc386f1-7944-4150-b718-958176706184)


  
- Deploy an application in the backend server
- e.g
   type <w3 schools html basics> on your browser and 
   pickup a basic applicaton code.
   - crate an index.html file and paste the code in it
        - vi index.html
   - Run the code using;
     - python3 -m http.server <port number>
     e.g python3 -m http.server 8000

![Screenshot 2025-06-17 163034](https://github.com/user-attachments/assets/51a05fe4-9504-414f-a8b4-4f7bc0d5b432)

           
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

  ![Screenshot 2025-06-17 165408](https://github.com/user-attachments/assets/8748bb25-aeb7-4cad-bf5b-a013e9a0241e)

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

     ![Screenshot 2025-06-17 165131](https://github.com/user-attachments/assets/89375cbd-a9d5-40c0-82e9-adb2e27abb72)

- Go back on your load balancer tab, select the target group
  you created.
- Click on Create load balancer

  ![Screenshot 2025-06-17 170712](https://github.com/user-attachments/assets/f8ba9b9c-20e2-47e9-8903-b76b57e51ff8)

 
- Check if access port is open on your load balancer SG
  - if not, open it.

- copy the load balancer DNS and access your application.

![Screenshot 2025-06-17 174329](https://github.com/user-attachments/assets/566faafd-c6a1-45c4-84b7-7f92f4af5fd8)



# Congratulations, you have successfully set a production grade environment on AWS with a secured application running on it    
