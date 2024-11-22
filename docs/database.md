### Step-by-Step Guide

Here is the step by step guide for deploying the Database instance of cognicity

- Download this [file](https://github.com/Climate-Emergency-Software-Alliance/cognicity-docs/blob/main/templates/rds.yml) in your local 
- Sign in to AWS console and open [Cloud  Formation](https://ap-southeast-1.console.aws.amazon.com/cloudformation/home?region=ap-southeast-1#/stacks?filteringText=&filteringStatus=active&viewNested=true) 
- Click on create stack -> Choose existing template -> Upload template file
- Follow the steps mentioned and add parameters accordingly
- If you need to create your own [VPC](https://github.com/Climate-Emergency-Software-Alliance/cognicity-docs/blob/main/templates/vpc.yml) [Security Groups](https://github.com/Climate-Emergency-Software-Alliance/cognicity-docs/blob/main/docs/security-group.md) Subnets using the above steps mentioned add those instead of the defaults mentioned below
  
| Parameter           | Value                                            |
|---------------------|--------------------------------------------------|
| Database instance   | {database-name-instance}                         |
| DBName              | {database-name}                                  |
| DBUser              | {username}                                       |
| DBPassword          | {password} (More than 8 characters)              |
| DBAllocatedStorage  | Change if needed or leave it to default          |
| DBInstanceClass     | Change if needed else leave it to default        |
| VPC                 | petabencana (vpc-0cf1288069ec1afb1) OR {YOUR-VPC}        |
| SecurityGroup       | rds (sg-019747b737ec5814c), rds-ec2-2 (sg-0154c3db60be6f9e4) OR {YOUR RDS [Security group] https://github.com/Climate-Emergency-Software-Alliance/cognicity-docs/blob/main/docs/security-group.md created} |
| SubnetIds           | subnet-0dd88600a96643d90, subnet-01e81f9673f37b27e, subnet-074efe765dfbeeaf1  OR {YOUR SUBNET IDS}|
