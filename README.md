# Elasticity in AWS EC2

> Developed for the Bachelor's Degree in Computer Science:
> - University: Universidade do Vale do Rio dos Sinos (Unisinos)
> - Subject: Distributed Systems
> - Semester: 2023/02
> - Students: Bel Cogo, Bruno Hoffmann and João Accorsi

# Objective

In a distributed system, elasticity is one of the most highlighted characteristics of Cloud Computing. It defines the degree to which the system is able to adapt to changes in workload, and through resource allocation, ensures that available resources are as close as possible to current demand. <br />

By this sample tutorial, elasticity concepts will be explored, related to how to configure it, and the expected outputs under AWS EC2 (Amazon Web Services Elastic Compute Cloud).

## 1. Create your AWS Account

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
| **Availability Zones and Subnets** | sa-east-1a and sa-east-1c (high availability) |
| **Group size > Desired Capacity** | 2 |
| **Group size > Minimum Capacity** | 2 |
| **Group size > Maximum Capacity** | 6 |

https://github.com/JoaoAccorsi/Elasticity-AWS-EC2/assets/60155867/332de211-a4a8-40bb-a432-9a0401db13d6

Once the above settings are completed, the two EC2 instances will be automatically created:

![3a  Create the Auto Scale Group](https://github.com/JoaoAccorsi/Elasticity-AWS-EC2/assets/60155867/6e5065cc-326a-4722-97d9-83467b389635)

In the Auto Scaling Group, create a Scheduled Action, so that the application will be monitored to apply the metrics:

https://github.com/JoaoAccorsi/Elasticity-AWS-EC2/assets/60155867/bcddad67-f5ec-4919-bb3d-52615f72bb5f

## 4. Create the Auto Scale Plan

The AWS Auto Scaling Plan defines how AWS will deal one a certain pre-configured parameter is reached. <br /> For example, raise one more instance once the CPU consumption reaches 80%.

✅ In the AWS top search bar, choose AWS Auto Scaling. <br />
✅ Choose EC2 Auto Scaling Groups. <br />
✅ Set the Auto Scaling Group as `auto-scaling-group-elasticity-in-AWS-EC2` (the one previously created). <br />
✅ Enter the Name as `scaling-plan-elasticity-in-AWS-EC2`. <br />
✅ Choose Auto Scaling Groups as custom. <br />
✅ Disable flag `Enable predictive scaling`. <br />
✅ Set Average CPU utilization by 80%.

https://github.com/JoaoAccorsi/Elasticity-AWS-EC2/assets/60155867/7d304a40-9959-437c-988e-1c29dcf236b5

By this Auto Scaling, once the Average CPU utilization reaches 80%, a new instance will be created in case it did not reach the maximum of 6 instances, defined in the `Auto Scale Group`. In the `Auto Scale Plan` it is also possible to see the graphic of the average CPU utilization:

![4a  Create the Auto Scale Plan](https://github.com/JoaoAccorsi/Elasticity-AWS-EC2/assets/60155867/5a271102-0dd2-48b9-bf07-357ff355a092)

## 5. Simulate Elasticity in AWS EC2

The configurations in AWS EC2 to explore its elasticity has been completed. <br />
To simulate, and further understand it, please consider:

## 5a. Access AWS EC2 Instance 

✅ Connect to the AWS EC2 instance via SSH.  <br />
  - This connection changes depending in the Operational System you are accessing with.  <br />
  - Refer to [How to Connect to an EC2 Instance Using SSH](https://www.clickittech.com/aws/connect-ec2-instance-using-ssh/).  <br />
  - For this tutorial, I am accessing AWS EC2 instance via Windows, so SSH PuTTY tool was used.
    
✅ Use EC2 user `ec2-user` to access the terminal. <br />
✅ Redo these steps for both the running instances.

https://github.com/JoaoAccorsi/Elasticity-AWS-EC2/assets/60155867/fa189f18-40c6-4a45-9630-07deb833519c

## 5b. Install some Linux tools in the Instances

To simulate the CPU stress, `stress` toll will be used. Also, to the the CPU consumption the instance, `htop` one. <br />

✅ Run the following commands in the terminal:

```linux
sudo yum update
sudo yum install stress
sudo yum install htop
```

![5b  Install some Linux tools in the instance](https://github.com/JoaoAccorsi/Elasticity-AWS-EC2/assets/60155867/d681d732-fb72-4a64-afd2-aeb7f084210d)

## 5c. Force the CPU Consumption

✅ Run the following command in the terminal of both instances to force the CPU consumption as 100%.

```linux
htop
stress --cpu 1
htop
```

![5c  Force the CPU consumption](https://github.com/JoaoAccorsi/Elasticity-AWS-EC2/assets/60155867/5aa7bef3-fc2c-4f86-b9ca-b7e163139f5c)

## 5d. Elasticity in Action

✅ The CPU consumption of AWS EC2 is in 100%. <br />
✅ It is above the configurable threshold of 80%. <br />
✅ AWS EC2 elasticity enters in action, and raise a new instance. <br />

![5da  Elasticity in Action](https://github.com/JoaoAccorsi/Elasticity-AWS-EC2/assets/60155867/66152e95-82b0-4bbe-a261-07c980432b50)

![5db  Elasticity in Action](https://github.com/JoaoAccorsi/Elasticity-AWS-EC2/assets/60155867/9dd4be36-75f9-4682-bf75-fb1aeb2f8f8f)

✅ Under the `Auto Scaling Groups` logs, the `Auto Scaling Plan` in action can be seen:

![5dc  Elasticity in Action](https://github.com/JoaoAccorsi/Elasticity-AWS-EC2/assets/60155867/293caa54-f624-4bac-9828-7846dd22e5d4)

## 5e. De-stressing the High CPU Consumption

✅ Hit `Ctrl C` in the instances terminals, stopping program `stress`.  <br />
✅ Wait some minutes.  <br />
✅ The `Auto Scaling Plan` detects that the CPU consumption is under the threshold of 80% again.  <br />
✅ The additional instances are terminated.  <br />

![5ea  De-stressing the High CPU Consumption](https://github.com/JoaoAccorsi/Elasticity-AWS-EC2/assets/60155867/f6e0b364-3931-4755-a272-abb7a87bccf0)

![5eb  De-stressing the High CPU Consumption](https://github.com/JoaoAccorsi/Elasticity-AWS-EC2/assets/60155867/1b780db9-1f0d-49c6-b0be-5b4a8c9df162)

![5ec  De-stressing the High CPU Consumption](https://github.com/JoaoAccorsi/Elasticity-AWS-EC2/assets/60155867/e2b411e4-288a-4e41-a448-bb74544f02e5)

## 6. Conclusion

Once configuring the `Launch Template`, `Auto Scale Group`, `Auto Scale Plan` and by some additional `Linux Commands`, in AWS EC2, the elasticity concept could be simulated, and put into action for learning proposes.

Nowadays, elasticity is crucial for all the application which requires high availability and response time, adapting the changes in workload, and through resource allocation, ensures that available resources are as close as possible to current demand.

So on, with this sample tutorial is was possible to further simulate understand it.
