---
layout: article
title: "Amazon Sagemaker at AWS re:invent 2024"
date: 2024-12-07
modify_date: 2024-12-07
excerpt: "Amazon Sagemaker new features"
tags: [AWS, Sagemaker, EMR, Redshift, Athena, Bedrock, MSK, Kinesis, OpenSearch, QuickSight]
mathjax: false
mathjax_autoNumber: false
key: aws-sagemaker-EMR-Redshift-athena-bedrock-msk-kinesis-opensearch-quicksight-tips
---

***

Given the recent popularity of **GenerativeAI** and Machine Learning workloads, AWS made a lot of announcements for SageMaker at AWS re:invent 2024. Here are a few highlights on [Amazon SageMaker](https://aws.amazon.com/sagemaker) last year.
Let's examine these in detail and attempt to clarify some of them.

## A.1

![Image](https://github.com/user-attachments/assets/1bf57255-16ce-40e3-9e2c-cc51975bd7f2)

The first one that was [SageMaker Unified Studio](https://aws.amazon.com/sagemaker/unified-studio/). It's a new service that provides an integrated experience for data preparation, model building, and generative AI application development that unifies your tools across notebooks, query editors, and services like [GLUE](https://aws.amazon.com/glue/), [EMR](https://aws.amazon.com/emr/), [Athena](https://aws.amazon.com/athena/), [Redshift](https://aws.amazon.com/redshift/), SageMaker, [BedRock](https://aws.amazon.com/bedrock/), [Managed Streaming Kafka](https://aws.amazon.com/msk/), [Kinesis](https://aws.amazon.com/kinesis/), [OpenSearch](https://aws.amazon.com/opensearch-service/), and it integrates seamlessly with our AWS data processing, using the actual existing services as part of the experience.

Customers today who are familiar with things like SQL Query Editor in Redshift or Athena, the Jupyter Notebook Experience in GLUE Studio, or the Experience in EMR Studio, or the existing SageMaker Studio, all of this tools is now available in the [Amazon SageMaker Unified Studio platform](https://aws.amazon.com/sagemaker/unified-studio/) so that **you can have one consistent notebook or query editor experience spanning across all of these different services with a single central UI.**

## A.2

![Image](https://github.com/user-attachments/assets/b4286695-dea3-4b6b-97cd-7e6aeb14a682)

Next, we have [Amazon SageMaker Lakehouse](https://aws.amazon.com/sagemaker/lakehouse/) announcement **that unifies your data across multiple sources for your analytics and AI initiatives with a single copy of data, regardless of how your data is stored**.

Data in S3 and Redshift is unified through one copy of data, functionally combining all of your transactional, warehouse, and data-like data into one system. The lakehouse is built on AWS Glue Data Catalog and Lake Formation. Data from the operational database, such as Amazon Aurora, RDS, and DynamoDB, are also available in the lakehouse. The zero ETL integrations with third-party SaaS applications, such as Salesforce, SAP, and ServiceNow, are available in the lakehouse once the zero ETL connections are sent up.

## A.3

![Image](https://github.com/user-attachments/assets/22693f62-a0de-4393-8f3c-ff013875402f)

Amazon Data Zones will work with the Amazon SageMaker catalog and the SageMaker Unified Studio to help with discovery, governance, and collaboration for data and AI across your lakehouse, AI models, and applications.

## A.4

![Image](https://github.com/user-attachments/assets/af3ee094-3dc8-4da0-90ed-831b7f365f67)

This is a major expansion of data that provides you with a unified view of your wider assets, not just your data, but also your ML and your AI models and your applications. You can now further coordinate with the creation of data assets, tracking of data lineage, manual, or ML automated documentation of business data descriptions. Search is also easier across your data and ML assets, with searches invoked from SageMaker Unified Studio or from the Amazon DataZone portal.

## A.5

![Image](https://github.com/user-attachments/assets/a67155b0-1b8f-4775-92b2-b73cb1302666)

Understanding data lineage is a common ask for many people. They think of lineage as the documented changes to the source data schema that can impact downstream transformation jobs or analytics, with the ability to audit data movement and access. 

Data lineage in DataZone and SageMaker Unified Studio will allow you to visualize your data's origins, transformations, and consumption so that you can enhance trust and verification of your data and those providing you the data, making it so that your evolving schemas are a lot more reliable.

## A.6

![Image](https://github.com/user-attachments/assets/83f67b15-1d7e-4d48-a692-831ac735b86f)

SageMaker Lakehouse is also **leveraging a unified connectivity to third party tools with this zero ETL connection**. There are additional service integrations between DynamoDB and SageMaker Lakehouse, as well as SaaS applications like Salesforce, SAP, Zendesk, and ServiceNow that provide an integrated access without building custom ETL pipelines. This is due to a new and existing glue connections and new connections from the SageMaker Unified Studio.

## A.7

![Image](https://github.com/user-attachments/assets/edfbb6e9-51bc-465e-9516-2259d666aa83)

AWS announced last year [SageMaker HyperPod](https://aws.amazon.com/fr/sagemaker-ai/hyperpod/). This is designed to streamline your distributed model training by effectively distributing your training activity across the accelerators in a cluster processing them in parallel.

The HyperPods training cluster is also resilient and self-healing and allows you to pause and inspect training jobs, which is usually a lot more complicated if you've never done that.

AWS know launched [SageMaker HyperPod Task governance](https://docs.aws.amazon.com/sagemaker/latest/dg/sagemaker-hyperpod-eks-operate-console-ui-governance.html), which will dynamically allocate compute resources and provide real-time analytics and insights of your compute allocation and utilization.

You can do things like define priorities, fine-tuning, training, and inference, and then you set up limits for the compute resources by teams and by projects.
You can easily reach thousands of different configurations of the training stack and training performance can be very significantly based on your chosen configurations.

## A.8

![Image](https://github.com/user-attachments/assets/068304ec-65ae-4ed0-a630-9bb5973668e7)

This year AWS introduced [SageMaker HyperPod Recipes](https://docs.aws.amazon.com/sagemaker/latest/dg/sagemaker-hyperpod-recipes.html) to provide a curated, ready-to-use, and customizable SageMaker recipe for pre-training and fine-tuning foundation models, models like llama, mistral, and so on. AWS will continue to add more recipes and more models to help you have a fully managed end-to-end training loop for those models.

