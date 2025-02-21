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
- [C. Build infrastructure](#c-build-infrastructure)

### A.What is Infrastructure as Code with Terraform?

Infrastructure as Code (IaC) tools allows you to:

- **Manage infrastructure with configuration files rather than through a graphical user interface** on multiple cloud platforms.
- **Build, change, and manage your infrastructure in a safe, consistent, and repeatable way by defining resource configurations that you can version, reuse, and share.**
- **Track resource changes throughout your deployments.**

#### A.1 Install terraform

For a full installation guide, see [Terraform Installation](https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli)

## C. Build infrastructure

With Terraform installed, you are ready to create your first infrastructure.

In this tutorial, you will provision an EC2 instance on Amazon Web Services (AWS). EC2 instances are virtual machines running on AWS, and a common component of many infrastructure projects.
