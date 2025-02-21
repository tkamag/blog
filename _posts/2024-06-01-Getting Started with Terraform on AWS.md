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
- [A.2 Provider Requirements](#a2-provider-requirements)
  - [A.2.1 AWS Provider](#a21-aws-provider)
    - [A.2.1.1 Configure AWS Provider](#a211-configure-aws-provider)
  - [A.2 Build infrastructure](#a2-build-infrastructure)

## A.What is Infrastructure as Code with Terraform?

Infrastructure as Code (IaC) tools allows you to:

- **Manage infrastructure with configuration files rather than through a graphical user interface** on multiple cloud platforms.
- **Build, change, and manage your infrastructure in a safe, consistent, and repeatable way by defining resource configurations that you can version, reuse, and share.**
- **Track resource changes throughout your deployments.**

### A.1 Install terraform

For a full installation guide, see [Terraform Installation](https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli)

## A.2 Provider Requirements

Terraform relies on plugins called ``providers`` to interact with remote systems. Terraform configurations must declare which providers they require, so that Terraform can install and use them. This [page documents](https://developer.hashicorp.com/terraform/language/providers/requirements) how to declare providers so Terraform can install them.

Additionally, some providers require configuration (like endpoint URLs or cloud regions) before they can be used. The [Provider Configuration](https://developer.hashicorp.com/terraform/language/providers/requirements) page documents how to configure settings for providers.

### A.2.1 AWS Provider

The [AWS Provider](https://registry.terraform.io/providers/hashicorp/aws/latest/docs) is used to provision resources on Amazon Web Services (AWS). You must configure the provider with the proper credentials before you can use it.

#### A.2.1.1 Configure AWS Provider

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

### A.2 Build infrastructure

With Terraform installed, you are ready to create your first infrastructure.

In this tutorial, you will provision an EC2 instance on Amazon Web Services (AWS). EC2 instances are virtual machines running on AWS, and a common component of many infrastructure projects.

