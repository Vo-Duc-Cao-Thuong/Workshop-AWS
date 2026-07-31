---
title: "Blog 3: Getting Started with AWS: An Introduction to Amazon S3"
date: 2026-07-24
weight: 3
chapter: false
pre: " <b> 3.3. </b> "
---

# Getting Started with AWS: An Introduction to Amazon S3

> _This article was shared by the author in the [AWS Study Group VN](https://www.facebook.com/groups/awsstudygroupfcj)._

When I first started learning AWS, one of the very first services I came across was Amazon S3. At first, I simply understood S3 as a place to store files in the cloud. However, after learning more about it, I realized that S3 is much more than just cloud storage—it is an essential component of many systems built on AWS.

In this article, I'd like to share what I've learned about Amazon S3 from the perspective of someone who is just getting started with AWS. If there is anything I misunderstand or miss, I would truly appreciate any feedback from the community.

### WHAT IS AMAZON S3?

Amazon S3 (Simple Storage Service) is AWS's object storage service.

On a personal computer, we usually organize files into folders. S3 works a little differently. Instead of folders, data is stored as **objects**, and these objects are organized inside **buckets**.

You can think of it this way:

- A **bucket** is a container that stores data.
- An **object** is an individual file stored inside a bucket.

For example, an e-commerce website might use Amazon S3 to store:

- Product images
- Videos
- Documents
- Files uploaded by users

The key difference is that instead of managing storage disks or storage servers yourself, AWS takes care of the underlying infrastructure.

### WHY NOT STORE EVERYTHING ON THE SERVER?

Before learning about cloud computing, I assumed a website could store everything on a single server:

- The application code
- The database
- Images and uploaded files

However, after learning how real-world systems are designed, I realized that separating these components provides many advantages.

For example:

- The backend focuses on business logic.
- The database stores structured data.
- Amazon S3 handles file storage.

This architecture makes the system easier to manage and much more scalable as the application grows.

### SOME BASIC CONCEPTS IN AMAZON S3

#### Bucket

A bucket is a container for storing objects in Amazon S3.

When using S3, the first step is usually creating a bucket where your data will be stored.

A bucket can contain many different types of data, although in practice developers often organize buckets according to their purpose.

Examples include:

- A bucket for website images
- A bucket for backup files
- A bucket for application data

### Object

An object is the basic unit of data stored in Amazon S3.

Each object consists of:

- The file content
- Metadata describing the file
- A key that uniquely identifies the object inside the bucket

For example, an image might have the following key:

`images/product01.png`

Instead of using a physical folder structure like a traditional file system, Amazon S3 uses the object key to organize and locate data.

### AMAZON S3 AND ACCESS CONTROL

One topic I found particularly important while learning S3 is security.

Initially, I thought storing files in the cloud was mainly about storage capacity and performance. In reality, controlling who can access your data is just as important.

AWS provides several mechanisms for access control, including:

- IAM for managing permissions for users and AWS services
- Bucket Policies for controlling access to buckets
- Access Control mechanisms for managing permissions on individual objects

For example:

A website may allow everyone to view product images, but personal user data should never be publicly accessible.

Learning about Amazon S3 helped me realize that storing data always goes hand in hand with managing access permissions.

### AMAZON S3 IS MORE THAN JUST FILE STORAGE

At first, I thought Amazon S3 was mainly useful for storing images and documents.

However, after exploring it further, I discovered that S3 is widely used for many other purposes, including:

- Backup storage
- System log storage
- Data storage for analytics
- File storage for web and mobile applications

Another interesting aspect is how well S3 integrates with other AWS services.

For example:

- An application stores uploaded files in Amazon S3.
- AWS Lambda processes data whenever a new file is uploaded.
- Amazon CloudFront delivers content to users with lower latency.

### WHAT I LEARNED WHILE EXPLORING AMAZON S3

The most interesting thing I discovered about Amazon S3 is that AWS doesn't simply provide a place to store data—it provides a flexible way to manage that data.

Initially, I viewed S3 as simply "a hard drive in the cloud." But after learning more, I realized that it is a key building block in the architecture of many modern applications.

For beginners learning AWS, I believe Amazon S3 is an excellent service to start with because it demonstrates one of the core ideas behind cloud computing: separating data storage from application processing.

### CONCLUSION

I'm still in the process of learning AWS, and Amazon S3 is just one of the first services I've explored.

By studying S3, I not only learned about an object storage service but also gained a better understanding of how cloud systems are designed—where each component has its own responsibility and works together with other services to build a complete solution.

These are my current thoughts and learnings about Amazon S3. If I've made any mistakes or if you have practical experience to share, I'd be grateful to hear your feedback.

### 📚 REFERENCES

- Amazon S3 Documentation:
  https://docs.aws.amazon.com/s3/

- Amazon S3 Overview:
  https://aws.amazon.com/s3/
