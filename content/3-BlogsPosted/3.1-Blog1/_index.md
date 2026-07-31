---
title: "Blog 1: After 2 months of learning AWS, how do I understand Amazon EC2?"
date: 2026-07-24
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

# After 2 months of learning AWS, how do I understand Amazon EC2?

> *Published on [AWS Study Group VN](https://www.facebook.com/groups/awsstudygroupfcj).*

Amazon EC2 was one of the first services I spent time exploring when I started learning AWS. This post is not a technical manual or an expert guide, but rather a reflection of what I have gathered and understood after 2 months of reading documentation, attending workshops, and self-learning. I hope it helps fellow beginners.

---

### STARTING WITH EC2

Opening the AWS Management Console for the first time felt quite overwhelming with unfamiliar service names like EC2, S3, IAM, VPC, and Lambda. However, EC2 kept popping up everywhere—from web hosting and backend servers to basic labs—which led me to focus on it first.

---

### EC2 IS NOT JUST A "VIRTUAL MACHINE"

Initially, I viewed EC2 simply as a virtual machine running in the cloud. While accurate, it felt too abstract.

I now view EC2 as "renting" a computer over the Internet, with complete flexibility to choose the OS, CPU, RAM, and storage allocation based on specific project needs—eliminating physical server maintenance.

---

### KEY HIGHLIGHTS

- **Instance Types:** Configured to match workload requirements rather than blindly picking top-tier specs, ensuring cost efficiency.
- **Security Groups:** Functions as the first-line firewall controlling inbound and outbound traffic, embedding security right from server creation.

---

### EVERYTHING IS CONNECTED IN THE AWS ECOSYSTEM

Exploring EC2 naturally introduced related services: **IAM** for access permissions, **VPC** for networking, and **CloudWatch** for resource monitoring. AWS services are designed to work together harmoniously.

---

### REFLECTIONS AFTER 2 MONTHS

Understanding *why* each service exists to solve specific problems makes learning AWS much more approachable.

**Reference Links:**
* **AWS Documentation – Amazon EC2 User Guide:** https://docs.aws.amazon.com/ec2/
* **Amazon EC2 – AWS Product Overview:** https://aws.amazon.com/ec2/
* **AWS Study Group Youtube:** https://www.youtube.com/@AWSStudyGroup
