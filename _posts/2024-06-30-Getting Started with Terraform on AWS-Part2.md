---
layout: article
title: "Getting Started with Terraform on AWS Part1"
date: 2024-06-30
modify_date: 2024-06-30
excerpt: "Terraform and Networking"
tags: [AWS, Terraform]
mathjax: false
mathjax_autoNumber: false
key: aws-terraform-tips
---
- [A.Networking for Applications](#anetworking-for-applications)
  - [A.1 - Create Public Subnet](#a1---create-public-subnet)
    - [A.1.1 - Public subnet - Data Source CIDR Subnet](#a11---public-subnet---data-source-cidr-subnet)
    - [A.1.2 - Public subnet - Internet Gateway (IGW)](#a12---public-subnet---internet-gateway-igw)
    - [A.1.3  Public subnet - Route Table (Associate route table to internet gateway)](#a13--public-subnet---route-table-associate-route-table-to-internet-gateway)
    - [Public subnet - Route table association](#public-subnet---route-table-association)


## A.Networking for Applications

To continue our series on Terraform on AWS, we will now focus on networking.

The ``${var.example}`` syntax is for including the result of an expression into a larger string. It is part of Terraform's string template syntax. For example, you might write 

````bash
${var.example}-foo 
````

to produce a string that consists of the value of **var.example** followed by the literal suffix **-foo**.

If you need only the value of the variable in isolation, without concatenating it with any other string values, there is no reason to use that interpolation syntax:

````bash
var.example    
${var.example} # are exactly equivalent.
````

For simple situations that Terraform can understand via basic syntactic analysis, ``terraform fmt`` will replace a redundant expression like 

````bash$
{var.example} 
````

with its simpler equivalent

````bash
var.example
````

That tool encodes various idiomatic style conventions like this, and so
it can be useful to apply the result of that tool (either directly by running it, or via its integration into plugins for editors like Visual Studio Code) to see if it makes an adjustment that would make your configuration style consistent with the usual idiomatic style.

### A.1 - Create Public Subnet

For High Availability we need multiple subnets spanning multiples availability zone. For making those subnets public, we have to create internet gateways (IGW) and configure them through route table.

````bash
- sh cidr_block = "${var.vpc_cidr}" : Returns the variable vpc_cidr define in variables.tf file.
````

- Variable define in ``dev.tfvars`` file are variable that is use in command line and those variables overwrite the one define in different file.

````bash
resource "aws_subnet" "public" {                          # Define resource with logical type and logical name
    count ="${length(local.az_names)}"                    # az_names is the list of the names of different az in the 
                                                          # region we work in.
    vpc_id = "${aws_vpc.my_app.id}"                       # Retrieve the Id of each VPC created
    cidr_block = cidrsubnet(var.vpc_cidr,8, count.index)  # Given a cidr_block, cidrsubnet will add 8 to a mask and 
                                                          # return one by one.
    availability_zone = "${local.az_names[count.index]}"  # count.index is to pick one by one element in a list starting at 0
    tags = {
     Name = "PublicSubnet-${count.index +1}"              # Here we will have for tags PublicSubnet-1, PublicSubnet-2, etc...
   }
}

````

#### A.1.1 - Public subnet - Data Source CIDR Subnet

- [Terraform Data Sources – How They Are Utilized](https://spacelift.io/blog/terraform-data-sources-how-they-are-utilised)

- [Managing AWS Security Groups Through Terraform](https://spacelift.io/blog/terraform-security-group)

**Data sources** help us import some informations (metadata) with is define outside terraform configurations

We'll use **Data sources** to fetch Availability zone from AWS account.

````bash
# Decare the data source
data "aws_availability_zones" "available" {
    state = "available"
}
````
This return all **availability zone** based on the region we're provisioning ressource.

When this Terraform configuration with appropriate provider settings is initialized and enabled, **Terraform** reads the information from AWS and makes it available in the ``data.aws_availability_zone.available`` variable.

To return all recent AWS AMI id from recent AWS, you can use:

````bash
data "aws_ami" "example" {
  most_recent = true
  owners      = ["self"]
  tags = {
    Name   = "app-server"
    Tested = true
  }
}
````

#### A.1.2 - Public subnet - Internet Gateway (IGW)

- [IGW - Resource](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/internet_gateway)
- [IGW - Data sources](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/internet_gateway)
  
````bash
resource "aws_internet_gateway" "igw" {
  vpc_id = aws_vpc.my_app.id

  tags = {
    Name = "Oliana-Igw"
  }
}
````

[![My image alt description](/blog/assets/images/posts-img/terraform/12.jpg)](/blog/assets/images/posts-img/terraform/12_.jpg)


[![My image alt description](/blog/assets/images/posts-img/terraform/13.jpg)](/blog/assets/images/posts-img/terraform/13.jpg)

#### A.1.3  Public subnet - Route Table (Associate route table to internet gateway)

- [Route table - Data Source](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/route_table)
- [Routes table - Data Source](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/route_tables)
- [Routes table - Resource](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/route_table)

````bash
resource "aws_route_table" "prt" {
  vpc_id = aws_vpc.my_app.id

  route {
    cidr_block = "0.0.0.0/0"
    gateway_id = aws_internet_gateway.igw.id
  }

  tags = {
    Name = "OlianaPRT"
  }
}
````

[![My image alt description](/blog/assets/images/posts-img/terraform/14.jpg)](/blog/assets/images/posts-img/terraform/14.jpg)


#### Public subnet - Route table association

- [Route Association - Resource](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/route_table_association)
- [IGW - Data sources](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/internet_gateway)