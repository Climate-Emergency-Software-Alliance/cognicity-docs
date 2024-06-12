## Deploying a new country to petabencana

Petabencana uses AWS for deploying the services all the services are currently deployed in Singapore region : 

This section gives an overview on the steps to follow for deploying a new country

## Prerequisites
Before you begin, ensure you have the following:
1. An AWS account.
2. IAM user with sufficient permissions to create and manage RDS instances.


### Step-by-Step Guide
### Step 1 : Sign and Open RDS
- Download this [file](https://github.com/Climate-Emergency-Software-Alliance/cognicity-docs/blob/main/templates/rds.yml) in your local 
- Sign in to AWS console and open [Cloud  Formation](https://ap-southeast-1.console.aws.amazon.com/cloudformation/home?region=ap-southeast-1#/stacks?filteringText=&filteringStatus=active&viewNested=true) 
- Click on create stack -> Choose existing template -> Upload template file
- Follow the steps mentioned and add parameters accordingly
  
| Parameter           | Value                                            |
|---------------------|--------------------------------------------------|
| Database instance   | {database-name-instance}                         |
| DBName              | {database-name}                                  |
| DBUser              | {username}                                       |
| DBPassword          | {password} (More than 8 characters)              |
| DBAllocatedStorage  | Change if needed or leave it to default          |
| DBInstanceClass     | Change if needed else leave it to default        |
| VPC                 | petabencana (vpc-0cf1288069ec1afb1)              |
| SecurityGroup       | rds (sg-019747b737ec5814c), rds-ec2-2 (sg-0154c3db60be6f9e4) |
| SubnetIds           | subnet-0dd88600a96643d90, subnet-01e81f9673f37b27e, subnet-074efe765dfbeeaf1 |


### Step 2 : Setup APIs
- Perquisites
  - Clone and setup the cognicity-serverless repo
  - Install serverless globally
    `npm i serverless -g`
  - Get a domain registered and make sure it is managed by Route53 
  - Request for an edge SSL certificate i.e *.{yourdomainname} in [ACM](https://us-east-1.console.aws.amazon.com/acm/home?region=us-east-1#/certificates/list).
  - Make sure to select **DNS validation** in the validation methods while requesting for the certificate
- Configure the env and serverless.yml file in coginicity-serverless repository
- Things to configure <br/><br/>
**serverless.yml**
    ```
    certificateArn : {YOUR-CERTIFICATE-ARN}
    ```
- We create two separate files for each environment i.e `dev.env.yml` for development and `prod.env.yml` for production
- Sample configuration for `env`, `dev.env.yml`, `prod.env.yml` files are present in this repository.
- Command to deploy . Make sure that you have setup the following correctly before running the command.
    - .env is available
    - dev.env.yml is configured
    - serverless.yml is configured with appropriate values

```
serverless deploy --stage {dev | prod} --param="service={SERVICE-TO-DEPLOY}"
```

For Example : You want to deploy reports service to dev environment we run the following

```
serverless deploy --stage dev --param="service=reports"
```
- After it is successfully deployed run go to [API Gateway](https://ap-southeast-1.console.aws.amazon.com/apigateway/main/apis?region=ap-southeast-1). Find the service deployed
- Add a new method to the base route
- Methods to add for some of the widely used services
  
| Service           | Method to add                                      |
|---------------------|--------------------------------------------------|
| cards   | POST           |
| reports              | GET                                 |

- The following needs to be configured in **Integration request** while adding the method 
    - Integration request type - Lambda
    - Lambda function - {YOUR-LAMBDA-FUNCTION-DEPLOYED}
    - Lambda proxy integration - True
