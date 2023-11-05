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

✅ In the AWS Console, go to the EC2 Launchpad. <br />
✅ Under Instances Tab, access Launch Templates. <br />
✅ Create the template with the below characteristics: <br />

| Configuration  | Setup
|---|---|
| **Launch Template Name** | template-elasticity-in-AWS-EC2 |
| **Template Version Description** | Template for the Elasticity Example in AWS EC2 |
| **Application and OS Images** | Quick Start > Amazon Linux AWS > Any free tier version |
| **Instance Type** | t2.micro |
| **Key pair** | Any key pair that you already have, or create a new one to access the Operating System |
| **Security Group** | Default |

https://github.com/JoaoAccorsi/Elasticity-AWS-EC2/assets/60155867/aabd5051-7a82-44c9-a2c5-86bc6f5c56b4

## 3. Create the Auto Scale Group

The AWS Auto Scaling continuously monitors applications to ensure they operate at desired performance levels.

✅ In the EC2 console, access Auto Scaling Group. <br />
✅ The most important setting for the elasticity setup is the capacities under the Group Size:

| Configuration  | Meaning
|---|---|
| **Desired Capacity** | Defines the desired number of instances that the system will have. |
| **Minimum Capacity** | Defines how many instances the system will always have. If the metrics are all fine, this would be how many instances will be running. |
| **Maximum Capacity** | Defines the maximum number of instances that the system may have, in case of high input load. |

✅ Create it with the below characteristics: <br />

| Configuration  | Setup
|---|---|
| **Auto Scaling Group Name** | auto-scaling-group-elasticity-in-AWS-EC2 |
| **Launch Template** | template-elasticity-in-AWS-EC2 |
| **Availability Zones and Subnets** | sa-east-1a and sa-east-1b (high availability) |
| **Group size > Desired Capacity** | 2 |
| **Group size > Minimum Capacity** | 2 |
| **Group size > Maximum Capacity** | 6 |

https://github.com/JoaoAccorsi/Elasticity-AWS-EC2/assets/60155867/332de211-a4a8-40bb-a432-9a0401db13d6

Once the above settings are completed, the two EC2 instances will be automatically created:

![3a  Create the Auto Scale Group](https://github.com/JoaoAccorsi/Elasticity-AWS-EC2/assets/60155867/02cd7922-90a2-4929-8c00-4812b576e327)

In the Auto Scaling Group, create a Scheduled Action, so that the application will be monitored to apply the metrics:

https://github.com/JoaoAccorsi/Elasticity-AWS-EC2/assets/60155867/bcddad67-f5ec-4919-bb3d-52615f72bb5f




