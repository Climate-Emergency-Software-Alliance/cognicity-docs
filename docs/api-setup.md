### Step-by-Step Guide

Here is the step by step guide for deploying the API's of cognicity

- Perquisites
  - Clone and setup the cognicity-serverless repo
  - Install serverless globally
    `npm i serverless -g`
  - Get a domain registered and make sure it is managed by Route53 
  - Request for an edge SSL certificate i.e *.{yourdomainname} in [ACM](https://us-east-1.console.aws.amazon.com/acm/home?region=us-east-1#/certificates/list).
  - Make sure to select **DNS validation** in the validation methods while requesting for the certificate

**Step 1** :
- Configure the env and serverless.yml file in coginicity-serverless repository
- Things to configure <br/><br/>
**serverless.yml**
    ```
    certificateArn : {YOUR-CERTIFICATE-ARN}
    ```
**Step 2** :
- We create two separate files for each environment i.e `dev.env.yml` for development and `prod.env.yml` for production
- Sample configuration for `env`, `dev.env.yml`, `prod.env.yml` files are present in this repository.

**Step 3** :
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

**Step 4** :
- After it is successfully deployed run go to [API Gateway](https://ap-southeast-1.console.aws.amazon.com/apigateway/main/apis?region=ap-southeast-1). Find the service deployed
- Add a new method to the base route
- Methods to add for some of the widely used services

| Service           | Method to add                                            |
|---------------------|--------------------------------------------------|
| cards   | POST           |
| reports              | GET      |


- The following needs to be configured in **Integration request** while adding the method 
    - Integration request type - Lambda
    - Lambda function - {YOUR-LAMBDA-FUNCTION-DEPLOYED}
    - Lambda proxy integration - True
