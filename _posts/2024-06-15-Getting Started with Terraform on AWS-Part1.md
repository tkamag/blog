---
layout: article
title: "Getting Started with Terraform on AWS Part1"
date: 2024-06-15
modify_date: 2024-06-15
excerpt: "Getting Started with Terraform on AWS Part1"
tags: [AWS, Terraform]
mathjax: false
mathjax_autoNumber: false
key: aws-terraform-tips
---
- [A.Creating Resources and Terraform Fundamentals](#acreating-resources-and-terraform-fundamentals)

## A.Creating Resources and Terraform Fundamentals

Before deep dive into creating resources, let's take a look at some prerequisites.

1. As we're working with ``git``, let's update our ``.gitignore`` file by adding this:

    ````bash
    # Local .terraform directories
    **/.terraform/*

    # .tfstate files
    *.tfstate
    *.tfstate.*

    # Crash log files
    crash.log
    crash.*.log

    # Exclude all .tfvars files, which are likely to contain sensitive data, such as
    # password, private keys, and other secrets. These should not be part of version 
    # control as they are data points which are potentially sensitive and subject 
    # to change depending on the environment.
    *.tfvars
    *.tfvars.json
    *.tfvars.example

    # Ignore override files as they are usually used to override resources locally and so
    # are not checked in
    override.tf
    override.tf.json
    *_override.tf
    *_override.tf.json

    # Include override files you do wish to add to version control using negated pattern
    # !example_override.tf

    # Include tfplan files to ignore the plan output of command: terraform plan -out=tfplan
    # example: *tfplan*

    # Ignore CLI configuration files
    .terraformrc
    terraform.rc
    ````

2. Let's create an alias in our ``.bashrc`` or ``.zshrc`` file:

    ```` bash
    echo -n "alias tf='terraform'" >> ~/.bashrc
    ````

    or

    ```` bash
    echo -n "alias tf='terraform'" >> ~/.zshrc
    ````

3. Create a folder ``Learn_Terraform_With_AWS`` and log in to that folder.

    ````bash
    mkdir Learn_Terraform_With_AWS && cd Learn_Terraform_With_AWS
    ````
