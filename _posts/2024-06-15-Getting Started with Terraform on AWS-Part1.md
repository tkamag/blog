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
  - [A.1.2 Terraform Local State file](#a12-terraform-local-state-file)
  - [A.1.3 Terraform Remote State file](#a13-terraform-remote-state-file)
  - [A.1.4 Terraform Local State file](#a14-terraform-local-state-file)
  - [A.1.5 Terraform Variables And tfvars](#a15-terraform-variables-and-tfvars)

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

### A.1.2 Terraform Local State file

All resources creates using Terraform script is maintain inside one JSON file format and called by default ``terraform.tfstate`` and the default location is your workspace.

When you hint ``terraform apply`` , it compare the terraform script with the state file.

> Any difference between the files would allow terraform to add, update or destroy ressource in the state file.
>
> If you delete your state file, whatever resource he's create previously, he's loose connexion to that. The ressource remain into your account but Terraform will not have access or control to that ressource.

### A.1.3 Terraform Remote State file

When many developers are working together on the same state file, it's very difficult to use a local state file.

- A good practice is to use S3 as a remote state file location and activate versioning on S3 bucket to keep previous version of the file.

- It's also a good practice to enable encryption.

- [S3 Backend.](https://developer.hashicorp.com/terraform/language/settings/backends/s3)

By adding this piece of code, the problem will be solve.

````bash
cat <<EOF > main.tf
  terraform {
    backend "s3" {
        bucket = "tfstate-bucket-tka-190"
        key    = "terraform.tfstate"
        region = "us-east-1"
  }
}
EOF
````

Note:

- You need to create a s3 bucket first by using aws cli or management console.
- After uploading your local state file to S3, you can delete the local file because terraform will not longer wse this local file, **it will only work with the remote file**.

Tips:

- The referenced S3 bucket must have been previously created. Otherwise you'll get into this error
  
````bash
Error: Failed to get existing workspaces: S3 bucket "tfstate-bucket-tka-19" does not exist.
│
│ The referenced S3 bucket must have been previously created. If the S3 bucket
│ was created within the last minute, please wait for a minute or two and try
│ again.
│
│ Error:    operation error S3: ListObjectsV2, 
│            https response error StatusCode: 404, 
│            RequestID: J2YFVD9K8JTHTA1R, 
│            HostID: ToWXadaZGcM5g2QYlR67Z+hoJ/wM/OhMxxw6cWBYLZ1Lvl73/S5IgsTQwI144wYaDajxpSyF3eI=, 
│            NoSuchBucket:
````

[![My image alt description](/blog/assets/images/posts-img/terraform/07.jpg)](/blog/assets/images/posts-img/terraform/07_.jpg)

### A.1.4 Terraform Local State file

If multiple developers applying concurrently, it can create inconsistent state file

> It's always important to make a lock when a developer is performing an operation on that and block the remaining users until the current operation is completed.

For state locking and consistency, we use a ``dynamo_db`` table.

- [DynamoDB State Locking](https://developer.hashicorp.com/terraform/language/settings/backends/s3#dynamodb-state-locking)

- The table must have a partition key named **LockID** with type of String. If not configured, state locking will be disabled.

````bash
cat <<EOF > main.tf
  terraform {
    backend "s3" {
        bucket = "tfstate-bucket-tka-1900"
        key    = "terraform.tfstate"
        region = "us-east-1"
        dynamodb_table = "table_name"
  }
}
EOF
````

### A.1.5 Terraform Variables And tfvars

In programmation, variables gives better maintainability and code reusability.

1. First create a new file called ``variables.tf``
1. In terraform the name of the file don't matter, only the extensions of the file.
1. **Don't forget to segregate you code into multiple small script**.

Note:

- [Variables and Outputs](https://developer.hashicorp.com/terraform/language/values)

````bash
cat <<EOF > providers.tf
    variable "vpc_cidr" {
        default = "10.20.0.0/18"
        description ="Choose cidr for VPC"
        type = string
}
EOF
````

- Here we have define a variable ``vpc_cidr`` with his default value, type and description. This value can be overwrite at the compilation using ``-var`` 

- Now we need to change ``providers.tf`` a lite bit.

[![My image alt description](/blog/assets/images/posts-img/terraform/09.jpg)](/blog/assets/images/posts-img/terraform/09_.jpg)

[![My image alt description](/blog/assets/images/posts-img/terraform/10.jpg)](/blog/assets/images/posts-img/terraform/10_.jpg)

Note:

- You can use command line extension ``-auto-complete`` to avoid the prompt when using terraform apply.
- To pass variables when using ``terraform apply``, use the command line ``-var "vpc_cidr=10.30.0.0/16"``
- When you have more than one variable, keep those value inside a file and pase the reference to that file using the comand line ``-var-file locatio_of_the_file``
- Whatever the name of the file you use, it is mandatory to have ``.tfvars`` as a file's extension.
