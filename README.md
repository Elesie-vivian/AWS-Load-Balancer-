 # AWS-Load-Balancer-
 ## OVERVIEW

 This project takes a look at Load balancers and autoscaling groups to gain practical experience in setting up these components on AWS. We will also configure Auto Scaling Groups to automatically adjust the number of instances based on demand.
 We will split this into two parts; Part 1 will cover setting up the Application Load Balancer while Part 2 will focus on configuring the Auto Scaling Groups.

 ### PART - 1

 First, we will create two EC2 instances with some web content.

 ![alt text](<Images/Image 1.1.PNG>)
 ![alt text](<Images/Image 1.PNG>)


 ![alt text](<Images/Image 2.PNG>)
 ![alt text](<Images/Image 3.PNG>)

  We then go further to create other components like Target Groups, Security groups etc.

 * A- Target Group

 On the EC2 Dashboard, we locate Target groups on the left side Panel and select "Create Target Group" then fill in the relevant fields to complete the configuration. This includes providing a name for the target group, set the protocol to HTTP,choose port no. as 80. 
 We will also choose the instances we have created to serve as targets for the application load balancer.

 ![alt text](<Images/Image 4.PNG>)


 * B- Creating Load Balancer

 1. Still on the EC2 page, we locate the load balancer service and click on it.
 select to create an Applcation Load Balancer, and proceed to fill the relevant fields to complete the process.

 Note: We created VPC for earlier projects which have two Public subnets in two availability zones, Internet gateway, security groups and route tables.
 We have also configured subnet association for the route table.
 These we use to complete the configuration.

 In the "Default action" section, we select the target group we created earlier and then proceed to create load balancer.

 ![alt text](<Images/Image 5.PNG>)

 After creating ALB (Application Load Balancer), we go to the target group and check the health of our instances.

 ![alt text](<Images/Image 6.PNG>)

 Note: If any of the instances are marked as unhealthy, its essential to first verify connectivity by attempting to ping the instances to confirm 
 network reachabilty.

 To view the Load Balancer content, we copy the DNS of the Load Balancer and paste on a web browser.
 We'll observe as we refreash the web page, that the load balancer is evenly distributing the workload across the two instances.

 ### PART - 2
 **A-  Creating Auto Scaling Group**

   * On the EC2 page, we locate Auto scaling Group on the left panel and click that to proceed.

   * Click on "create auto scaling group"

   * We click "create a launch template". Right click to open in a new tab to launch template.
   ( This is where we create a template for the instances to be created by the auto scaling group).
   
   _Follow the steps below to create a launch template:_

   * In the network setting we'll select the public subnets that we created earlier.
   * select the "Enable" option for auto-assigning public IP addresses.
   * In the "Advanced details" section, we'll input some user data which contains a HTML file with a welcome message.
   * Then proceed to create launch template.

    Back to the Auto Scaling Group page,
  
  a. We select the launch template we created above.

  b. Choose the required instance attributes

  c. Also select the VPC created earlier as well as Availability zones.

  d. Next, we configure "Advanced options", select "Attach to an existing load balancer"

  e. Then proceed to fill other relevant fields to complete the configuration to create Auto Scaling Group.

  ![alt text](<Images/Image 7.PNG>)

  Now, we click on the Auto scaling Group above and navigate to the "Instance Management" section, 

 ![alt text](<Images/Image 8.PNG>)

  Observe that the Auto scaling Group has successfully created instances according to the desired capacity specified, in this case 2.

  If we want to see the websites, we'll again use the load balancer DNS.

 ![alt text](<Images/Image 9.PNG>)

  We'll observe the behaviour when one of the instances created by the Auto Scaling Group(ASG) is deleted, simulating an uhealthy instance.

  ![alt text](<Images/Image 10.PNG>)

  In response, a new instance is created by the Auto Scaling Group to maintain the desired state of instances.

  ![alt text](<Images/Image 11.PNG>)

  ![alt text](<Images/Image 12.PNG>)

  This demonstrates the dynamic nature of ASG which adjusts the number of instances based on the configured capacity settings.
