# AWS EC2 Master Class ( with auto scaling and load balancing) - Udemy
## Objectives and Overview
![images](https://github.com/KennySoh/Technical-Interview/blob/master/oop/EC2_1.png). 
![images](https://github.com/KennySoh/Technical-Interview/blob/master/oop/EC2_2.png)
## EC2 Basic
### What is EC2?
***
- Renting Virutal Machines (EC2)
- Storing data on virtual drives (EBS)
- Distributing load across machines (ELB)
- Scaling the services using an auto-scaling group (ASG)
***
### Launcing an EC2 Instance running Linux
***
1) Go to amazon management console
2) Choose the region
3) Go to EC2
4) Launch Instance
4a) Can check ur Service Health
4b) [Step 1]Choose your Amazon Machine Image (AMI), The operating system, application server and application configs
4b) [Step 2]Choose an instance type
4b) [Step 3]Config instance details
4b) [Step 4]Add storage
4b) [Stepb 6]Config Security Group
4b) Key pair

***

### Security Group 
***
![images](https://github.com/KennySoh/Technical-Interview/blob/master/oop/EC2_3.png)
***

### Private vs Public ip 
- IPv4 (Most Common) vs IPv6 ( More of newer iot systems)

### EC2 User Data (Bootstrap scipt)
- Only run once.... can use it to reset configurations. 
```
to automate server instance creation
```
### AMI
Its an Image we can use for faster server instance creation

