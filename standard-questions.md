## Standard Interview Questions

### Q1. What is Cloud Computing? 

**Answer:**  Cloud computing is the delivery of computing resources such as servers, storage, databases, networking, and applications over the internet on demand. Instead of purchasing and maintaining physical infrastructure, organizations can provision resources from cloud providers such as AWS and pay based on usage.

### Q2. What are the major advantages of cloud computing? 

**Answer:**  The major advantages include: ● Scalability – resources can be increased or decreased based on demand. ● Cost efficiency – organizations can avoid large upfront infrastructure costs. ● High availability – applications can be designed across multiple Availability Zones. ● Global reach – resources can be deployed in different AWS Regions. ● Flexibility – infrastructure can be provisioned quickly. ● Automation – resources can be managed using APIs, CLI, and infrastructure-as-code tools.

### Q3. What is the difference between scalability and elasticity? 

**Answer:**  Scalability is the ability of a system to handle increased workload by adding resources. Elasticity goes further by automatically increasing or decreasing resources according to workload demand. For example, an application using Auto Scaling can add EC2 instances during high traffic and remove them when traffic decreases.

### Q4. What is an AWS account? 

**Answer:**  An AWS account provides an isolated environment in which AWS resources are created and managed. It provides boundaries for resources, billing, permissions, and security controls.

### Q5. Why should you avoid using the AWS root user for daily operations? 

**Answer:**  The root user has extensive privileges over the AWS account. For daily operations, it is better to use appropriate IAM identities and roles with only the permissions required for the task. MFA should also be enabled to strengthen account security.

### Q6. What is IAM in AWS? 

**Answer:**  IAM stands for Identity and Access Management. It allows administrators to control: ● Who can access AWS ● Which AWS resources they can access ● Which actions they can perform IAM includes concepts such as users, groups, roles, and policies.

### Q7. What is the principle of least privilege? 

**Answer:**  The principle of least privilege means giving a user, application, or service only the permissions required to perform its intended task. For example, if a developer only needs to start and stop EC2 instances, they should not automatically receive full administrator permissions.

### Q8. What is an AWS Region? 

**Answer:**  An AWS Region is a separate geographic area containing multiple AWS data center locations known as Availability Zones. Organizations select Regions based on factors such as: ● User proximity ● Compliance requirements ● Service availability ● Cost ● Disaster recovery strategy

### Q9. What is an Availability Zone? 

**Answer:**  An Availability Zone, or AZ, is an isolated location within an AWS Region. A Region typically contains multiple Availability Zones designed to provide isolation from failures in other AZs.

### Q10. Why would you deploy an application across multiple Availability Zones? 

**Answer:**  Deploying across multiple AZs improves availability and fault tolerance. If one Availability Zone experiences an infrastructure problem, resources in another AZ can continue serving users.

### Q11. What is an IP address? 

**Answer:**  An IP address is a logical address used to identify a device or network interface and enable communication over an IP network. An IPv4 address is represented using four decimal numbers, for example: 10.0.1.10

### Q12. What is CIDR? 

**Answer:**  CIDR stands for Classless Inter-Domain Routing. It represents an IP network using an IP address and prefix length. Example: 10.0.0.0/16 The /16 indicates that the first 16 bits represent the network portion.

### Q13. What are the private IPv4 address ranges? 

**Answer:**  The standard private IPv4 ranges are: 10.0.0.0/8 172.16.0.0/12 192.168.0.0/16 These ranges are commonly used for internal networks and AWS VPCs.

### Q14. What is the difference between a public IP and a private IP? 

**Answer:**  A private IP is used for communication within private networks and is not directly routable over the public internet. A public IP can be used for communication over the internet, provided the required routing and security configuration exists.

### Q15. What is an AWS VPC? 

**Answer:**  Amazon VPC, or Virtual Private Cloud, is a logically isolated virtual network in AWS. It allows you to control: ● IP address ranges ● Subnets ● Route tables ● Internet connectivity ● Network security

### Q16. What are the main components of a VPC? 

**Answer:**  Important VPC components include: ● VPC CIDR block ● Subnets ● Route tables ● Internet Gateway ● NAT Gateway ● Security Groups ● Network ACLs Depending on the architecture, other components such as VPC peering and endpoints may also be used.

### Q17. What is an Internet Gateway? 

**Answer:**  An Internet Gateway, or IGW, is a VPC component that provides a path between a VPC and the internet. For a resource to communicate with the internet, appropriate routing and addressing must also be configured.

### Q18. What is a route table? 

**Answer:**  A route table contains routing rules that determine where network traffic should be sent. Example: Destination Target 0.0.0.0/0 Internet Gateway This route sends IPv4 traffic destined outside the VPC through the Internet Gateway.

### Q19. What makes a subnet public? 

**Answer:**  A subnet is considered public when its associated route table has a route to an Internet Gateway. For example: 0.0.0.0/0 → Internet Gateway Resources in the subnet also need appropriate IP addressing and security configuration to communicate with the internet.

### Q20. What makes a subnet private? 

**Answer:**  A private subnet does not have a direct route to an Internet Gateway. If resources in the private subnet require outbound internet access, the subnet can route traffic through a NAT Gateway.

### Q21. What is a NAT Gateway? 

**Answer:**  A NAT Gateway allows resources in private subnets to initiate outbound connections to the internet without giving those resources direct internet connectivity. Typical traffic flow: Private EC2
↓
Private Route Table
↓
NAT Gateway
↓
Internet Gateway
↓
Internet

### Q22. What is Amazon EC2? 

**Answer:**  Amazon EC2, or Elastic Compute Cloud, provides resizable virtual compute capacity in AWS. An EC2 instance can be used to run: ● Web applications ● APIs ● Backend services ● Development environments ● Enterprise applications

### Q23. What is an AMI? 

**Answer:**  AMI stands for Amazon Machine Image. An AMI provides the information required to launch an EC2 instance, including the operating system and potentially software/configuration depending on how the image was created.

### Q24. What is a Security Group in AWS? 

**Answer:**  A Security Group is a stateful virtual firewall associated with supported AWS resources such as EC2 network interfaces. It controls allowed inbound and outbound network traffic.

### Q25. What is the difference between a Security Group and a NACL? 

**Answer:**  Security Group NACL Stateful Stateless Associated with network interfaces/resources Associated with subnets Supports allow rules Supports allow and deny rules Return traffic is automatically allowed Return traffic must be explicitly permitted Resource-level control Subnet-level control
