Table of Contents
=================

* [Introduction](#introduction)
* [Prerequisite](#Prerequisite)
* [Project-Structure](#Project-Structure)
* [Development](#Development)



## Introduction

Implement GitOps with AWS using GitHub Actions(workflows) to automate the deployment of your infrastructure and application to AWS via cloudformation. In the example GitHubs actions will serve as the CI/CD tools trigging deployment to AWS when changes are pushed to main branch of the repository

## Prerequisite

1. AWS Account: Ensure you have an AWS account set up.
2. AWS CLI: Install and configure the AWS Command Line Interface.
3. Git Repository: Have a Git repository set up for your application code and infrastructure as code (IaC) templates.
4. GitHub Actions or another CI/CD tool like GitLab CI, CircleCI, etc.( In belowe exaple we are not using any CI/CD tools)
5. Store AWS Credential in GitHub Secrets like aws_access_key_id and aws_secreat_access_key

## Project Structure

├── gitops-example          <- GitOps example project directory
│   ├── clouldformation.yaml    <- cloudformation example
|   ├── iam_role.json       <- IAM role with admin needed to run cloudformation
|   ├── .github          <- Github action workflow folder
│       ├── workflows   <- Github action workflow folder
|           ├── deploy.yml       <- workflow yml file


## Development