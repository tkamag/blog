---
layout: article
title: "What is Amazon Redshift?"
date: 2023-01-24
modify_date: 2023-01-24
excerpt: "Is Amazon Redshift only a data warehouse product?"
tags: [AWS, Redshift]
mathjax: false
mathjax_autoNumber: false
key: aws-redshift-tips
---

***

## Amazon Redshift

Just a quick overview, what is Amazon Redshift ?

**Amazon redshift** is a **fully managed asset compliant cloud Datawarehouse service** provided by AWS that offers fast and predictable performance with seamless scalability. So ten of thousands of customers are using Redshift today.
{:.info}

**Amazon Redshift** is very optimize, in fact he has this **MPP architecture** i.e that's **Massive Paralell Precessing Architecture**. What you are getting at is, whith **Amazon Redshift** today, it support open files formats like **parquet, JSON, csv, ORC** and because of it **MPP** ypu get all the performance you need.

<figure>
  <img src="https://user-images.githubusercontent.com/14333637/214537112-3a6ec816-f578-4975-8a5e-e5f6d7c3d0c8.png" alt=".." title="Optional title" width="70%" height="70%"/>
	<figcaption></figcaption>
</figure>


Amazon Redshift is:

1. A **SQL compliant cloud datawarehouse**

2. He has **petabyte-scale capacity**, that means that Redshift datawarehouse, a single cluster can be pentabyte scale i.e it can store pentabyte of data inside this datawerouse solution. 
>So you can run complex queries and analytics and it work with data data visualization tools as well and others services(S3, DynamoDB, Kinesis, EMR)

> For customers, it's **SOC** compliance, **SOC 1**, **SOC 2**, **SOC 3**, **HIPAA**, **FedRAMP**  and lot mores, and give you an **SLA** of 99.9 % i.g if an entire cluster a single node goes down, it doesn't means that you will lose all your data because of how the architecture is and how it mirrors data to a secondary node.

3. **Amazon Redshift** is basically base on open-source **postgres** database but it's completely rewritten and very cost efficient compared to traditionnal on-premises datawarehouse because customers here are not doing any maintenance of infrastructure, management at all.

> To summarize, **Redshift** it has a **massively  parallel processing architecture** but to put it in a very simple terms, **one job is broken into small jobs and it's distributed accross different nodes
 to gives you result faster**.

 So if you have long running query and large processing jobs, it really speed performance.

<figure>
  <img src="https://user-images.githubusercontent.com/14333637/214536365-9b395b90-adbb-48d6-9a01-d55607bd9bc4.png" alt=".." title="Optional title" width="70%" height="70%"/>
	<figcaption></figcaption>
</figure>

* `Amazon Redshift` has a **columnar storage** so it's very good when it comes to run analytics you don't have this data written in the form of rows. 
* >> **Data from each column is stored together so the data can be accessed faster, without scanning and sorting all other columns** 
* **Each node has its own storage, its own compute and it's independent of other nodes in the cluster** so there are not going to be single point of failures what it also means is **you can easily add new nodes in the cluster or remove based on your required.** 

***

## Item 2: Amazon Redshift architecture

<figure>
  <img src="https://user-images.githubusercontent.com/14333637/214539972-bc2767d6-239a-41e9-9025-cdcf4804ee6b.png" alt=".." title="Optional title" width="70%" height="70%"/>
	<figcaption></figcaption>
</figure>

What we are looking at is a Redshift cluster and this Redshift cluster is made-up of **leader nodes** that is a **single leader node** and **multiple compute nodes** it could be a single compute node or more than one compute node. 

Your client applications(if they want to analyze and run analytical queries), could use a JDBC connectivity or ODBC connectivity to your Redshift cluster(leader node).So:

a. Client application connect to the leader node

b. Leader node gets all of those queries from the client applications 

c. Leader node **uses a mechanism to spread the queries across compute nodes**, get the results back aggregate those results and then give it back to the client 
> This is a the **basic overview of this architecture or Redshift architecture** 

### Leader node

<figure>
  <img src="https://user-images.githubusercontent.com/14333637/214544314-8020a60f-a8b1-4aad-842b-7f5c02b4e179.png" alt=".." title="Optional title" width="70%" height="70%"/>
	<figcaption></figcaption>
</figure>

`Amazon redshift` cluster consists of 1 leader node and it could have multiple compute nodes. 
- This leader node is automatically provisioned and customers do not pay for this, 
- it's **completely managed by AWS** and **automatically provisioned in every cluster**,  
+ Customers are not charged for the leader node and this leader node is basically your SQL entry point for your clients or for BI tools to access the cluster


There are two types of secondary index in DynamoDB:

- **Global secondary index (GSI)**: An index with a **partition key** and a **sort key** that can be different from those on the base table.
  - A global secondary index is considered "global" because queries on the index can span all of the data in the base table, across all partitions.
- **Local secondary index (LSI)**: An index that has the **same partition key** as the base table, but a **different sort key**.
  - A local secondary index is "local" in the sense that every partition of a local secondary index is scoped to a base table partition that has the same partition key value.

So the basic difference is the "scope" of each index is different. GSI has the global view while LSI has view only those data share the same partition key

When you use these two types of indexes, there is also a difference when you try to retrieve data back

1. LSI supports Strongly Consistency and Eventual Consistency
   1. which will always return the latest version of records if you can enable this by changing the `ConsistentRead` property when sending out a query
2. GSI supports Eventual Consistency
   1. which might return a stale version of records, and you dont have the option to enable strong consistency

So, how can I choose the correct DDB index? I found this flow chart very helpful:

![](https://user-images.githubusercontent.com/6509926/72526710-a66b7c80-382c-11ea-8923-dbb9c9589881.png)

> Image source: https://www.dynamodbguide.com/local-or-global-choosing-a-secondary-index-type-in-dynamo-db/#the-too-long-didnt-read-version-of-choosing-an-index


## Item 3: `SaveBehavior` Configuration

When you use DynamoDB for CRUD operations, you will find out that DynamoDB does not have the actual "Update" concept. However, there is a `SaveBehavior` configuration which serves as the missed role in DynamoDB. Let's take a look.

```java
DynamoDBMapper mapper = new DynamoDBMapper(dynamoDBClient);

// SaveBehavior.UPDATE is the default value
mapper.save(something, new DynamoDBMapperConfig(SaveBehavior.UPDATE));
```

There are four different configurations for `SaveBehavior`

- `UPDATE` (default)
- `UPDATE_SKIP_NULL_ATTRIBUTE`
- `CLOBBER`
- `APPEND_SET`

Given this existing record and DynamoDB schema

| AttributeName 	| key    	| modeled_scalar 	| modeled_set 	| unmodeled 	|
|---------------	|--------	|----------------	|-------------	|-----------	|
| KeyType       	| Hash   	| Non-key        	| Non-key     	| Non-key   	|
| AttributeType 	| Number 	| String         	| String set  	| String    	|

```json
{
    "key" : "99",
    "modeled_scalar" : "foo", 
    "modeled_set" : [
        "foo0", 
        "foo1"
    ], 
    "unmodeled" : "bar" 
}
```

together with this POJO class object

```java
TestTableItem obj = new TestTableItem();
obj.setKey(99);
obj.setModeledScalar(null);
obj.setModeledSet(Collections.singleton("foo2");
```

***

**`SaveBehavior.UPDATE`**

`UPDATE` will not affect unmodeled attributes on a save operation, and a `null` value for the modeled attribute will **remove** it from that item in DynamoDB.

so basically after onvoking `mapper.save()`, the record in DDB will be as follows

```json
{
  "key" : "99",
  "modeled_set" : [
    "foo2"
  ], 
  "unmodeled" : "bar" 
}
```

You can see that `modeled_set` has been updated, but since `modeled_scalar` is passed in using a `null` value, so it is removed from DDB.

In this case. if you wanna use `SaveBehavior.UPDATE` to update something, you have to include all the fields with proper value in your DynamoDB POJO class. Otherwise, it will be removed from DDB table instead of keep them as is.

***

**`SaveBehavior.UPDATE_SKIP_NULL_ATTRIBUTES`**

`UPDATE_SKIP_NULL_ATTRIBUTES` is similar to `UPDATE`, except that it ignores any `null` value attribute(s) and will **NOT** remove them from that item in DynamoDB.

```json
{
  "key" : "99",
  "modeled_scalar" : "foo",
  "modeled_set" : [
    "foo2"
  ], 
  "unmodeled" : "bar" 
}
```

As you can find out, even though we set `modeled_scalar` to be `null`, this field is still persisted in DDB. So with this configuration, when you trying to update something with only specifying the hashKey and the field you wanna alter, it will properly update the field and keep the others the same without deleting.

***

**`SaveBehavior.CLOBBER`**

CLOBBER will _clear and replace all attributes_, including unmodeled ones

> (delete and recreate) on save.

```json
{
  "key" : "99", 
  "modeled_set" : [
    "foo2"
  ]
}
```

This is already self-explained. delete the record with same hashKey and re-create a new one with the specified fields.

***

**`SaveBehavior.APPEND_SET`**

`APPEND_SET` treats scalar attributes (String, Number, Binary) the same as UPDATE_SKIP_NULL_ATTRIBUTES does.

However, for **set attributes, it will append to the existing attribute value**, instead of overriding it.


```json
{
  "key" : "99",
  "modeled_scalar" : "foo",
  "modeled_set" : [
    "foo0", 
    "foo1", 
    "foo2"
  ], 
  "unmodeled" : "bar" 
}
```

Scalar attributes are kept, but set attributes are appended.

***

| SaveBehavior                	| On unmodeled attribute 	| On null-value attribute 	| On set attribute 	|
|-----------------------------	|------------------------	|-------------------------	|------------------	|
| UPDATE                      	| keep                   	| remove                  	| override         	|
| UPDATE_SKIP_NULL_ATTRIBUTES 	| keep                   	| keep                    	| override         	|
| CLOBBER                     	| remove                 	| remove                  	| override         	|
| APPEND_SET                  	| keep                   	| keep                    	| append           	|


## References

- [Best Practices for Querying and Scanning Data](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/bp-query-scan.html)
- [Local or global: Choosing a secondary index type in DynamoDB](https://www.dynamodbguide.com/local-or-global-choosing-a-secondary-index-type-in-dynamo-db/#the-too-long-didnt-read-version-of-choosing-an-index)
- [Using the SaveBehavior Configuration for the DynamoDBMapper](https://aws.amazon.com/blogs/developer/using-the-savebehavior-configuration-for-the-dynamodbmapper/)
