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
  - [A.1 Creating Resources](#a1-creating-resources)
  - [A.1.1 Terraform Output](#a11-terraform-output)

## A.Creating Resources and Terraform Fundamentals

Before deep dive into creating resources, let's take a look at some prerequisites.

1. Assume you've already configure your aws cli.
2. As we're working with ``git``, let's update our ``.gitignore`` file by adding this:

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

3. Let's create an alias in our ``.bashrc`` or ``.zshrc`` file:

    ```` bash
    echo -n "alias tf='terraform'" >> ~/.bashrc
    ````

    ```` bash
    echo -n "alias tf='terraform'" >> ~/.zshrc
    ````

4. Create a folder ``Learn_Terraform_With_AWS`` and log in to that folder.

    ````bash
    mkdir Learn_Terraform_With_AWS && cd Learn_Terraform_With_AWS
    ````

5. Before crating some resources, we need to define and configure providers in our ``providers.tf`` file.

    ````bash
    cat <<EOF > providers.tf
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
    EOF
    ````

[![My image alt description](/blog/assets/images/posts-img/terraform/02.jpg)](/blog/assets/images/posts-img/terraform/02_.jpg)

After adding providers details, you have to initialize Terraform project by running terraform init

- ``terraform init`` will download providers plugins and will create a .terraform folder in your workspace.

- ``terraform init`` are not run very often , but each time it is run, it will download the version of the specified provider.

[![My image alt description](/blog/assets/images/posts-img/terraform/03.jpg)](/blog/assets/images/posts-img/terraform/03_.jpg)

### A.1 Creating Resources

For creating resources, let's first create a file name ``main.tf`` and add the following code.

````bash
cat <<EOF > main.tf
    resource "aws_vpc" "my_vpc" {
        cidr_block = "10.0.0.0/16"
        instance_tenancy = "default"

        tags = {
            Name        = "Oliana-Vpc"
            Environment = "Dev"
            Location    = "Paris - France"
        }
    }
EOF
````

The structure of Terraform resource is:

- ``resource`` the key world
- The type of resource we are interest in ``aws_vpc``
- Logical name ``my_vpc``

Documentation:

- Resource: [aws_vpc](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/vpc)
- Resource: [Argument Reference](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/vpc#argument-reference) are argument uses to define a vpc resource.
- Resource: [Attribute Reference](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/vpc#attribute-reference) are argument return after creating the vpc

Now we can apply those changes by running terraform apply.

````bash
terraform apply      
````

````bash
tf apply      
````

- Execute all scripts in the current folder
- Give us the plan detail and all actions that will be perform.

[![My image alt description](/blog/assets/images/posts-img/terraform/04.jpg)](/blog/assets/images/posts-img/terraform/04_.jpg)

And voila

[![My image alt description](/blog/assets/images/posts-img/terraform/05.jpg)](/blog/assets/images/posts-img/terraform/05.jpg)

Note:

- If we run again ``terraform apply``, nothing will happens because resources has already been created.
- Any change in the code(add more tags, change cidr block, etc...) will update our ressource.

### A.1.1 Terraform Output

Suppose we want to print the ``cidr block`` after ``terraform apply`` is complete, we need to modify a bit our code by adding this piece of code in our ``main.tf`` :

````bash
output "vpc_cidr" {
    value = "${aws_vpc.my_vpc.cidr_block}" 
}
````

[![My image alt description](/blog/assets/images/posts-img/terraform/06.jpg)](/blog/assets/images/posts-img/terraform/06_.jpg)
