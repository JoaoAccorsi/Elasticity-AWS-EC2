# Elasticity in AWS EC2

> Developed for the Bachelor's Degree in Computer Science:
> - University: Universidade do Vale do Rio dos Sinos (Unisinos)
> - Subject: Distributed Systems
> - Semester: 2023/02
> - Students: Bel Cogo, Bruno Hoffmann and João Accorsi

# Objective

In a distributed system, elasticity is one of the most highlighted characteristics of Cloud Computing. It defines the degree to which the system is able to adapt to changes in workload, and through resource allocation, ensures that available resources are as close as possible to current demand. <br />

By this sample tutorial, we will explore elasticity concepts, how to configure it, and the expected outputs under AWS EC2 (Amazon Web Services Elastic Compute Cloud).

## 1. Create your AWS account

Amazon Web Services (AWS) is a platform of Cloud Computing services offered by Amazon.com in various geographic areas around the world.

✅ Register (if needed) for the free tear account: [AWS Free Tier](https://aws.amazon.com/free/?trk=d0b462ed-a9ff-4714-8a75-634758c49d4c&sc_channel=ps&ef_id=Cj0KCQjw-pyqBhDmARIsAKd9XIOb-rhX0ce5hpe-7IZn3ObRddaGpEZHkMFbCtnjh3rFDg-_Uvq_DBUaAgusEALw_wcB:G:s&s_kwcid=AL!4422!3!531081610038!e!!g!!aws%20free%20vps%20server!12024810921!121376982932&all-free-tier.sort-by=item.additionalFields.SortRank&all-free-tier.sort-order=asc&awsf.Free%20Tier%20Types=*all&awsf.Free%20Tier%20Categories=*all). <br />
✅ Sign In with your AWS account: [AWS Console](https://aws.amazon.com/?nc1=h_ls).

## 2. Create the Lauch Template

This template defines the image for the creation of the Virtual Machines.

✅ In the AWS Console, go to the EC2 launchpad. <br />
✅ Under Instances Tab, access Launch Templates. <br />
✅ Create the template with the below characteristics: <br />

| Configuration  | Setup
|---|---|
| **Launch Template Name** | Elasticity-in-AWC-EC2 |
| **Template Version Description** | Sample Elasticity Example in AWS EC2 |
| **Application and OS Images (Amazon Machine Image)** | Quick Start > Amazon Linux AWS > Any free tier version |
| **Instance Type** | t2.micro |
| **Key pair** | Any key pair that you already have, or create a new one |
| **Security Group** | Default |

## 3. Define the Auto Scale Group
