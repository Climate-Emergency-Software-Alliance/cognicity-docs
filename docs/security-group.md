## Security Groups to be created

1. **RDS (For connecting postgres)**
  - Go to [Security Groups](https://ap-southeast-1.console.aws.amazon.com/vpcconsole/home?region=ap-southeast-1#SecurityGroups) and 
    click on Create new Security Group
  -  Add the following Inbound and Outbound Rules
  - <img width="1114" alt="inbound" src="https://github.com/user-attachments/assets/fd6c4b33-80ae-4722-867b-f6dd66ddd296">
  Outbound Rules
  - ![image](https://github.com/user-attachments/assets/36dec898-f871-448b-8ec5-7ed95ab5140a)
    
2. **Serverless**
  - Click on create new security group
  -  Add the following Outbound Rules and leave Inbound Rules empty
  -  ![image](https://github.com/user-attachments/assets/b7a18572-0b54-4c4d-8454-5deb8d6b6304)
  - Go back to RDS security group , Click on Edit Inbound Rules and add this security group as source ,
    as seen in Inbound Rules image of RDS security group
    
3. **SSH ( For giving SSH access )**
  -  Click on create new security group
  -  Add the following Inbound Rules
  -  ![image](https://github.com/user-attachments/assets/1de88542-3177-4cfc-b2aa-4a84e6e00d8a)
  -  Outbound Rules
  - ![image](https://github.com/user-attachments/assets/b7a18572-0b54-4c4d-8454-5deb8d6b6304)

4. **Lambda-Invoke ( For allowing traffic to invoke lambda inside serverless APIs )**
  - Click on create new security group
  -  Add the following Inbound Rules
  ![image](https://github.com/user-attachments/assets/1a30cebc-ef69-4be2-a04c-60a3d7a05dd4)
  Outbound Rules
  ![image](https://github.com/user-attachments/assets/bcb1f725-29f1-4657-a495-4f0f9a46b37d)

Note : In additon to this we have to create a few endpoints to allow services such as s3 and Lambda to be accessed inside APIs

### Endpoints
Prequistes
  - Go to Internet Gateways and create a new Internet Gateway and attach your VPC to it
  - Go to Route tables and click on create Route Table and click on Edit routes and add the following
    ![image](https://github.com/user-attachments/assets/72c373eb-99c0-4d03-b9b7-67333563523e)

1. s3-VPC-Endpoint
 - Go to Endpoints under VPC side menu and create a new endpoint with the following selected
 - ![image](https://github.com/user-attachments/assets/5effb567-f2d8-4c87-820a-ce852e9fa056)
 - Select the VPC you have created and would like to attach - Should be the same VPC you are using for RDS
 - Select the route table you have created above

2. lambda-invoke
  -  Go to Endpoints under VPC side menu and create a new endpoint with the following selected
  -  ![image](https://github.com/user-attachments/assets/2eabbbae-b50f-42b3-b142-fde07153ebb2)
  -  Select the VPC you have created and would like to attach - Should be the same VPC you are using for RDS
  -  Attach Lambda-Invoke security group you have created above


