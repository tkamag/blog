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
  - [B.2 Environment Variables](#b2-environment-variables)
    - [B.2.1 Shared Configuration and Credentials Files](#b21-shared-configuration-and-credentials-files)
- [C. Resources](#c-resources)
- [D. Initialize the directory](#d-initialize-the-directory)
  - [D.1 Format and validate the configuration](#d1-format-and-validate-the-configuration)
- [E. Build infrastructure](#e-build-infrastructure)
- [F. Inspect state](#f-inspect-state)
  - [F.1 Manually Managing State](#f1-manually-managing-state)
- [G. Destroy infrastructure](#g-destroy-infrastructure)

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

### B.2 Environment Variables

Credentials can be provided by using the ``AWS_ACCESS_KEY_ID, AWS_SECRET_ACCESS_KEY``, and optionally A``WS_SESSION_TOKE``N environment variables. The region can be set using the ``AWS_REGION`` or ``AWS_DEFAULT_REGION`` environment variables.

For example:

````terraform
provider "aws" {}
% export AWS_ACCESS_KEY_ID="anaccesskey"
% export AWS_SECRET_ACCESS_KEY="asecretkey"
% export AWS_REGION="us-west-2"
% terraform plan
````

#### B.2.1 Shared Configuration and Credentials Files

The AWS Provider can source credentials and other settings from the shared configuration and credentials files. By default, these files are located at:

````terraform
- $HOME/.aws/config and $HOME/.aws/credentials on Linux and macOS, and

- "%USERPROFILE%\.aws\config" and "%USERPROFILE%\.aws\credentials" on Windows.
````

If no named profile is specified, the default profile is used. Use the profile parameter or AWS_PROFILE environment variable to specify a named profile.

The locations of the shared configuration and credentials files can be configured using either the parameters shared_config_files and shared_credentials_files or the environment variables ``AWS_CONFIG_FILE`` and ``AWS_SHARED_CREDENTIALS_FILE``.

For example:

````terraform
provider "aws" {
  shared_config_files      = ["/Users/tf_user/.aws/conf"]
  shared_credentials_files = ["/Users/tf_user/.aws/creds"]
  profile                  = "customprofile"
}
````

## C. Resources

Use resource blocks to define components of your infrastructure.

> A resource might be a physical or virtual component such as an EC2 instance, or it can be a logical resource such as a Heroku application.

Resource blocks have two strings before the block:

- The resource type here **aws_instance**
  
- The resource name here **app_server**

## D. Initialize the directory

When you create a new configuration (or check out an existing configuration from version control), you need to initialize the directory with ``terraform init``.

> Initializing a configuration directory downloads and installs the providers defined in the configuration, which in this case is the aws provider.

Initialize the directory.

````terraform
terraform init

Initializing the backend...

Initializing provider plugins...
- Finding hashicorp/aws versions matching "~> 4.16"...
- Installing hashicorp/aws v4.17.0...
- Installed hashicorp/aws v4.17.0 (signed by HashiCorp)

Terraform has created a lock file .terraform.lock.hcl to record the provider
selections it made above. Include this file in your version control repository
so that Terraform can guarantee to make the same selections by default when
you run "terraform init" in the future.

Terraform has been successfully initialized!

You may now begin working with Terraform. Try running "terraform plan" to see
any changes that are required for your infrastructure. All Terraform commands
should now work.

If you ever set or change modules or backend configuration for Terraform,
rerun this command to reinitialize your working directory. If you forget, other
commands will detect it and remind you to do so if necessary.
````

1. Terraform downloads the aws provider and installs it in a **hidden subdirectory** of your current working directory, named ``.terraform``.
1. The ``terraform init`` command prints out which version of the provider was installed.
1. Terraform also creates a lock file named ``.terraform.lock.hcl`` **which specifies the exact provider versions used**, so that you can control when you want to update the providers used for your project.

### D.1 Format and validate the configuration

We recommend using consistent formatting in all of your configuration files. The ``terraform fmt`` **command automatically updates configurations in the current directory for readability and consistency**.

Format your configuration. Terraform will print out the names of the files it modified, if any. In this case, your configuration file was already formatted correctly, so Terraform won't return any file names.

````terraform
 terraform fmt
 ````

You can also make sure your configuration is syntactically valid and internally consistent by using the terraform validate command.

Validate your configuration. The example configuration provided above is valid, so Terraform will return a success message.

````terraform
terraform validate
Success! The configuration is valid.
 ````

## E. Build infrastructure

Apply the configuration now with the ``terraform apply`` command. Terraform will print output similar to what is shown below. We have truncated some of the output to save space.

````terraform
 terraform apply

Terraform used the selected providers to generate the following execution plan.
Resource actions are indicated with the following symbols:
  + create

Terraform will perform the following actions:

   aws_instance.app_server will be created
  + resource "aws_instance" "app_server" {
      + ami                          = "ami-830c94e3"
      + arn                          = (known after apply)
#...

Plan: 1 to add, 0 to change, 0 to destroy.

Do you want to perform these actions?
  Terraform will perform the actions described above.
  Only 'yes' will be accepted to approve.

  Enter a value:
````

Before it applies any changes,

> Terraform prints out the execution plan which describes the actions Terraform will take in order to change your infrastructure to match the configuration.

````terraform
  Enter a value: yes

aws_instance.app_server: Creating...
aws_instance.app_server: Still creating... [10s elapsed]
aws_instance.app_server: Still creating... [20s elapsed]
aws_instance.app_server: Still creating... [30s elapsed]
aws_instance.app_server: Creation complete after 36s [id=i-01e03375ba238b384]

Apply complete! Resources: 1 added, 0 changed, 0 destroyed.
````

## F. Inspect state

When you applied your configuration, Terraform wrote data into a file called ``terraform.tfstate``.

Terraform stores the IDs and properties of the resources it manages in this file, so that it can update or destroy those resources going forward.
The Terraform state file is the only way Terraform can track which resources it manages, and often contains sensitive information, so you must store your state file securely and restrict access to only trusted team members who need to manage your infrastructure.

> In production, we recommend storing your state remotely with Terraform Cloud or Terraform Enterprise.

Terraform also supports several other remote backends you can use to store and manage your state.
Inspect the current state using terraform show.

````terraform
terraform show

# aws_instance.app_server:
resource "aws_instance" "app_server" {
    ami                          = "ami-830c94e3"
    arn                          = "arn:aws:ec2:us-west-2:561656980159:instance/i-01e03375ba238b384"
    associate_public_ip_address  = true
    availability_zone            = "us-west-2c"
    cpu_core_count               = 1
    cpu_threads_per_core         = 1
    disable_api_termination      = false
    ebs_optimized                = false
    get_password_data            = false
    hibernation                  = false
    id                           = "i-01e03375ba238b384"
    instance_state               = "running"
    instance_type                = "t2.micro"
    ipv6_address_count           = 0
    ipv6_addresses               = []
    monitoring                   = false
    primary_network_interface_id = "eni-068d850de6a4321b7"
    private_dns                  = "ip-172-31-0-139.us-west-2.compute.internal"
    private_ip                   = "172.31.0.139"
    public_dns                   = "ec2-18-237-201-188.us-west-2.compute.amazonaws.com"
    public_ip                    = "18.237.201.188"
    secondary_private_ips        = []
    security_groups              = [
        "default",
    ]
    source_dest_check            = true
    subnet_id                    = "subnet-31855d6c"
    tags                         = {
        "Name" = "ExampleAppServerInstance"
    }
    tenancy                      = "default"
    vpc_security_group_ids       = [
        "sg-0edc8a5a",
    ]

    credit_specification {
        cpu_credits = "standard"
    }

    enclave_options {
        enabled = false
    }

    metadata_options {
        http_endpoint               = "enabled"
        http_put_response_hop_limit = 1
        http_tokens                 = "optional"
    }

    root_block_device {
        delete_on_termination = true
        device_name           = "/dev/sda1"
        encrypted             = false
        iops                  = 0
        tags                  = {}
        throughput            = 0
        volume_id             = "vol-031d56cc45ea4a245"
        volume_size           = 8
        volume_type           = "standard"
    }
}
````

### F.1 Manually Managing State

Terraform has a built-in command called ``terraform state`` **for advanced state management**. Use the list subcommand to list of the resources in your project's state.

````terraform
 terraform state list
aws_instance.app_server
````

## G. Destroy infrastructure

You have now created and updated an EC2 instance on AWS with Terraform. In this tutorial, you will use Terraform to destroy this infrastructure.
Destroy the resources you created.

````terraform
terraform destroy
Terraform used the selected providers to generate the following execution plan.
Resource actions are indicated with the following symbols:
  - destroy

Terraform will perform the following actions:

# aws_instance.app_server will be destroyed
  - resource "aws_instance" "app_server" {
      - ami                          = "ami-08d70e59c07c61a3a" -> null
      - arn                          = "arn:aws:ec2:us-west-2:561656980159:instance/i-0fd4a35969bd21710" -> null
##...

Plan: 0 to add, 0 to change, 1 to destroy.

Do you really want to destroy all resources?
  Terraform will destroy all your managed infrastructure, as shown above.
  There is no undo. Only 'yes' will be accepted to confirm.

  Enter a value:
  ````
  
The - prefix indicates that the instance will be destroyed. As with apply, Terraform shows its execution plan and waits for approval before making any changes.

Answer **yes** to execute this plan and destroy the infrastructure.

Enter a value: **yes**

````terraform
aws_instance.app_server: Destroying... [id=i-0fd4a35969bd21710]
aws_instance.app_server: Still destroying... [id=i-0fd4a35969bd21710, 10s elapsed]
aws_instance.app_server: Still destroying... [id=i-0fd4a35969bd21710, 20s elapsed]
aws_instance.app_server: Still destroying... [id=i-0fd4a35969bd21710, 30s elapsed]
aws_instance.app_server: Destruction complete after 31s

Destroy complete! Resources: 1 destroyed.
````
