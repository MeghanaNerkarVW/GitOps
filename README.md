Table of Contents
=================

* [Project-Overview](#Project-Overview)
* [Prerequisite](#Prerequisite)
* [Project-Structure](#Project-Structure)
* [Development](#Development)
* [Documentation](#Documentation)


## Project-Overview

This project demonstrates the implementation of GitOps principles to manage infrastructure and application using AWS Cloudformation. By leveraging Git as the source of truth, changes to infrastructure are automated and deployed seamlessly through CI/CD pipeline.


## Prerequisite

1. AWS Account: Ensure you have an AWS account set up.
2. AWS CLI: Install and configure the AWS Command Line Interface.
3. Git Repository: Have a Git repository set up for your application code and infrastructure as code (IaC) templates.
4. GitHub Actions understanding or CI/CD tool understanding like GitLab CI, CircleCI, etc.(In below example we are not using any CI/CD tools)
5. Store AWS Credential in GitHub Secrets like aws_access_key_id and aws_secreat_access_key


## Project Structure

GitOps
├── .github                                 <- Github action workflow folder
│   ├── workflows                           <- Github action workflow folder
|     ├── deploy.yml                        <- workflow yml file
├── deployments                             <- GitOps example project directory
│   ├── dev                                 <- Environment folder
│   │   ├── clouldformation.yaml            <- cloudformation template for dev env
│   ├── staging                             
│   │   ├── clouldformation.yaml            <- cloudformation template for staging env
│   ├── prod                                
│   │   ├── clouldformation.yaml            <- cloudformation template for prod env
|   ├── iam_role.json                       <- IAM role with admin access needed to run cloudformation of AWS
├── docs                                    <- Documents folder
├── README.md                               <- Readme file for project understanding



## Development

Steps to Set Up GitOps with GitHub Actions and AWS CloudFormation

1. Create a GitHub Repository

Store your application code and AWS CloudFormation templates in a GitHub repository. You will use this repository to trigger GitHub Actions workflows.

2. Set Up an AWS IAM User for GitHub Actions

You’ll need to create an IAM user in AWS with programmatic access so that GitHub Actions can interact with AWS resources.

In the AWS Management Console, go to IAM > Users > Add user.

Create a new user with Programmatic access and attach the following policies (adjust as needed):
AmazonS3FullAccess (or limited S3 permissions)
AWSCloudFormationFullAccess
AWSCodeDeployFullAccess (if needed)
Custom permissions depending on the resources you’re managing via CloudFormation.

Please refer to the example in deployments/iam_role.json for further details.

3. Generate Access Key ID and Secret Access Key for this IAM user. You need store these credentials in GitHub secrets.

4. Store AWS Credentials in GitHub Secrets. To allow GitHub Actions to access AWS resources, store your AWS credentials as GitHub Secrets:
    1. Go to your GitHub repository.
    2. Navigate to Settings > Secrets and variables > Actions.
    3. Add the following secrets:
        AWS_ACCESS_KEY_ID
        AWS_SECRET_ACCESS_KEY
        Optionally, add AWS_REGION as a secret (e.g., us-east-1).

5. Create a GitHub Action Workflow

In your GitHub repository, create a .github/workflows/deploy.yml file that contains your GitHub Actions workflow configuration. This workflow will trigger on changes to your repository and deploy your infrastructure to AWS using CloudFormation.

Refer an example workflow that deploys a CloudFormation stack.
.github -> workflows -> deploy.yml

Example Determine step dynamically sets the environment based on the branch name.

6. Code Building

Build the cloudformation template or application code in folder structure mention in repo

Refer deployments -> dev/prod/staging -> cloudformation.yaml 
Example contains environment-specific configurations (e.g., dev, staging, production) for deploying infrastructure using CloudFormation. Each folder includes a cloudformation.yaml file defining AWS resources, eg. as S3 buckets. You can modify these templates to meet your requirements, like changing resource names or adding new resources. The deployment process is automated via the CI/CD pipeline in the .github/workflows/deploy.yml file.

5. Trigger the Workflow

This GitHub Actions workflow will trigger whenever you push changes to the your branch. Here's how it works:

actions/checkout@v3: Checks out your repository so the workflow can access your CloudFormation templates and application code.

aws-actions/configure-aws-credentials@v2: Configures the AWS CLI within the runner using your GitHub Secrets (AWS_ACCESS_KEY_ID, AWS_SECRET_ACCESS_KEY, and AWS_REGION).

aws cloudformation deploy: This command deploys the CloudFormation template. If the stack does not exist, it will be created. If it exists, it will be updated.


## Documentation

Detailed explanation about GitOps and CI/CD tools can be found in the docs folder.

docs/gitops.md: For a general overview on what is GitOps and where it can be used.

docs/cd_tools.md: This section explains the different CI/CD tools that can be incorporated into your pipeline for efficient GitOps functionality.