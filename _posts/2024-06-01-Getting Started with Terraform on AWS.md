---
layout: article
title: "Getting Started with Terraform on AWS"
date: 2024-06-01
modify_date: 2024-06-10
excerpt: "Getting Started with Terraform on AWS"
tags: [AWS, Terraform]
mathjax: false
mathjax_autoNumber: false
key: aws-terraform-tips
---
- [A.What is Infrastructure as Code with Terraform?](#awhat-is-infrastructure-as-code-with-terraform)
  - [A.1 Install terraform](#a1-install-terraform)
- [B. Provider Requirements](#b-provider-requirements)
  - [B.1 AWS Provider](#b1-aws-provider)
    - [B.1.1 Configure AWS Provider](#b11-configure-aws-provider)
    - [B.1.2 Authentication and Configuration](#b12-authentication-and-configuration)
    - [B.1.3 Provider Configuration](#b13-provider-configuration)
    - [B.1.4 Environment Variables](#b14-environment-variables)
    - [B.1.6 Shared Configuration and Credentials Files](#b16-shared-configuration-and-credentials-files)
  - [A.2 Build infrastructure](#a2-build-infrastructure)

## A.What is Infrastructure as Code with Terraform?

Infrastructure as Code (IaC) tools allows you to:

- **Manage infrastructure with configuration files rather than through a graphical user interface** on multiple cloud platforms.
- **Build, change, and manage your infrastructure in a safe, consistent, and repeatable way by defining resource configurations that you can version, reuse, and share.**
- **Track resource changes throughout your deployments.**

### A.1 Install terraform

For a full installation guide, see [Terraform Installation](https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli)

## B. Provider Requirements

Terraform relies on plugins called ``providers`` to interact with remote systems. Terraform configurations must declare which providers they require, so that Terraform can install and use them. This [page documents](https://developer.hashicorp.com/terraform/language/providers/requirements) how to declare providers so Terraform can install them.

Additionally, some providers require configuration (like endpoint URLs or cloud regions) before they can be used. The [Provider Configuration](https://developer.hashicorp.com/terraform/language/providers/requirements) page documents how to configure settings for providers.

### B.1 AWS Provider

The [AWS Provider](https://registry.terraform.io/providers/hashicorp/aws/latest/docs) is used to provision resources on Amazon Web Services (AWS). You must configure the provider with the proper credentials before you can use it.

#### B.1.1 Configure AWS Provider

Terraform 0.13 and later:

````terraform
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 5.0"
    }
  }
}

# Configure the AWS Provider
provider "aws" {
  region = "us-east-1"
}

# Create a VPC
resource "aws_vpc" "example" {
  cidr_block = "10.0.0.0/16"
}
````

#### B.1.2 Authentication and Configuration

Configuration for the AWS Provider can be derived from several sources, which are applied in the following order:

1. Parameters in the provider configuration
1. Environment variables
1. Shared credentials files
1. Shared configuration files
1. Container credentials
1. Instance profile credentials and region

#### B.1.3 Provider Configuration

**Warning:**
> Hard-coded credentials are not recommended in any Terraform configuration and risks secret leakage should this file ever be committed to a public version control system.


Credentials can be provided by adding an access_key, secret_key, and optionally token, to the aws provider block.

**Usage:**

````terraform
provider "aws" {
  region     = "us-west-2"
  access_key = "my-access-key"
  secret_key = "my-secret-key"
}
````

#### B.1.4 Environment Variables

Credentials can be provided by using the ``AWS_ACCESS_KEY_ID, AWS_SECRET_ACCESS_KEY``, and optionally A``WS_SESSION_TOKE``N environment variables. The region can be set using the ``AWS_REGION`` or ``AWS_DEFAULT_REGION`` environment variables.

For example:

````terraform
provider "aws" {}
% export AWS_ACCESS_KEY_ID="anaccesskey"
% export AWS_SECRET_ACCESS_KEY="asecretkey"
% export AWS_REGION="us-west-2"
% terraform plan
````

#### B.1.6 Shared Configuration and Credentials Files

The AWS Provider can source credentials and other settings from the shared configuration and credentials files. By default, these files are located at:

````terraform
- $HOME/.aws/config and $HOME/.aws/credentials on Linux and macOS, and

- "%USERPROFILE%\.aws\config" and "%USERPROFILE%\.aws\credentials" on Windows.
````

If no named profile is specified, the default profile is used. Use the profile parameter or AWS_PROFILE environment variable to specify a named profile.

The locations of the shared configuration and credentials files can be configured using either the parameters shared_config_files and shared_credentials_files or the environment variables AWS_CONFIG_FILE and AWS_SHARED_CREDENTIALS_FILE.

For example:

````terraform
provider "aws" {
  shared_config_files      = ["/Users/tf_user/.aws/conf"]
  shared_credentials_files = ["/Users/tf_user/.aws/creds"]
  profile                  = "customprofile"
}
````









### A.2 Build infrastructure

With Terraform installed, you are ready to create your first infrastructure.

In this tutorial, you will provision an EC2 instance on Amazon Web Services (AWS). EC2 instances are virtual machines running on AWS, and a common component of many infrastructure projects.

