### Step-by-Step Guide

We have to frontend repositories to deploy 1. Riskmap and 2. Cards

Here is the step by step guide for deploying the Frontend repositories of cognicity.

- Perquisites
    - Assuming you already have a domain and SSL certificate configured in Route53 and ACM respectively

**Step 1 : Configure CloudFront for both repositories**
- Download this [file](https://github.com/Climate-Emergency-Software-Alliance/cognicity-docs/blob/main/templates/cloudfront.yml) in your local 
- Sign in to AWS console and open [Cloud  Formation](https://ap-southeast-1.console.aws.amazon.com/cloudformation/home?region=ap-southeast-1#/stacks?filteringText=&filteringStatus=active&viewNested=true) 
- Click on create stack -> Choose existing template -> Upload template file
- Follow the steps mentioned and add parameters accordingly
  
| Parameter           | Value                                            |
|---------------------|--------------------------------------------------|
| Bucket Name   | {YOUR-BUCKET-NAME} - Suggested: {name-of-the-app}-{name-of-the-repository i.e Riskmap|Cards}                         |
| CertificateARN              | {YOUR-ACM-Certificate-ARN}                                  |

**Note : This step should be followed for both the repositories i,e for Riskmap and Cards**

**Step 2: Configuring Route53** :
- After creating the the CloudFront distribution. Make note of the **Distribution domain name** of the created cloudfront distribution.
- Create ***A*** and ***AAA*** records in Route53 with value as CloudFront **Distribution domain name**
- This should be done for both ***{domain-name}*** and ***cards.{your-domain-name}***

**Step 3: Setting up the CodePipeline**
- We have to create 2 Pipeline's one for Riskmap and the other for Cards