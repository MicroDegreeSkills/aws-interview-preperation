## Scenario-Based Questions

### Q1. Your company has an EC2 instance in a private subnet. It needs to download software updates from the internet. How would you design this? 

**Answer:**  I would use a NAT Gateway. The NAT Gateway would be placed in a public subnet. The private subnet's route table would contain: 0.0.0.0/0 → NAT Gateway The public subnet containing the NAT Gateway would have a route to the Internet Gateway. This allows the EC2 instance to initiate outbound internet connections without assigning it a public IP.

### Q2. An EC2 instance is deployed in a public subnet, but users cannot access the website. How would you investigate? 

**Answer:**  I would check the complete connectivity path: 1. EC2 instance status 2. Web server status 3. Application listening port 4. Security Group inbound rules 5. NACL rules 6. Route table 7. Internet Gateway 8. Public IP configuration 9. Operating system firewall I would verify each layer rather than assuming the issue is with the Security Group.

### Q3. Your organization wants users to access a web application from the internet, but the application servers should not have public IP addresses. What architecture would you use? 

**Answer:**  I would use an internet-facing load balancer in public subnets and keep the application servers in private subnets. Internet
↓
Load Balancer
↓
Private Application Servers Security Groups would allow the application servers to receive traffic only from the load balancer where appropriate.

### Q4. Your database should never be directly accessible from the internet. How would you design the network? 

**Answer:**  I would place the database in private subnets without public internet exposure. The application servers would communicate with the database over private networking. I would also configure Security Groups so that the database accepts traffic only from the required application layer.

### Q5. Your application receives extremely high traffic during a sale and one EC2 instance cannot handle the load. What would you recommend? 

**Answer:**  I would use horizontal scaling. A typical design would include: Internet
↓
Application Load Balancer
↓
Auto Scaling Group
  ├── EC2
  ├── EC2
  └── EC2 The number of EC2 instances can be increased during high demand and reduced when demand falls.

### Q6. Your application must remain available even if one Availability Zone fails. What would you change? 

**Answer:**  I would deploy application resources across multiple Availability Zones. For example: Load Balancer / \ AZ-1 AZ-2 | | EC2 EC2 This removes dependency on a single Availability Zone.

### Q7. An EC2 instance in a private subnet cannot access the internet. The instance itself is running normally. What would you investigate? 

**Answer:**  I would check: ● Private subnet route table ● Route to NAT Gateway ● NAT Gateway availability ● NAT Gateway public subnet ● Public subnet route to Internet Gateway ● Security Groups ● NACLs ● DNS configuration The complete outbound path needs to be valid.

### Q8. Your private EC2 instance can access an external IP address but cannot access a website using its domain name. What would you investigate? 

**Answer:**  I would investigate DNS resolution. I would check the DNS configuration and use tools such as nslookup or dig to determine whether the hostname is resolving correctly. Because the instance can reach an external IP, basic outbound connectivity may already be working.

### Q9. A developer accidentally configured SSH access from 0.0.0.0/0. What would you do? 

**Answer:**  I would immediately restrict the SSH rule. Instead of allowing: TCP 22 → 0.0.0.0/0 I would allow SSH only from a trusted administrative IP range or use a secure management solution such as Systems Manager where appropriate. I would also review logs to determine whether unauthorized access occurred.

### Q10. An EC2 web server is running, but port 80 is unreachable. The Security Group allows port 80. What would you check next? 

**Answer:**  I would check: ● Whether the application is actually listening on port 80 ● OS firewall ● NACL ● Route table ● Internet Gateway ● Public IP ● Web server configuration A correct Security Group does not guarantee that the application is reachable.

### Q11. Your NACL allows inbound traffic, but the connection still fails. What is a likely issue? 

**Answer:**  Because NACLs are stateless, the return traffic must also be explicitly allowed. I would check the outbound NACL rules, including the ports required for the response traffic.

### Q12. Two VPCs need to communicate privately. What would you implement? 

**Answer:**  If the requirements are suitable and the CIDR ranges do not overlap, I would consider VPC Peering. I would: 1. Create the peering connection. 2. Accept it if required. 3. Add routes to both VPC route tables. 4. Update Security Groups. 5. Check NACLs. 6. Test private connectivity.

### Q13. VPC Peering is active, but EC2 instances in the two VPCs cannot communicate. What would you check? 

**Answer:**  I would verify: ● Routes in both VPCs ● Destination CIDRs ● Peering connection as the route target ● Security Groups ● NACLs ● OS firewalls ● Instance private IPs ● CIDR overlap The peering connection alone does not automatically configure routing.

### Q14. Two VPCs use 10.0.0.0/16 and 10.0.0.0/16. The team wants to establish VPC Peering. What would you tell them? 

**Answer:**  The CIDR ranges overlap, so the VPCs cannot be peered directly. The organization should use non-overlapping address ranges when designing VPCs for connectivity. For example: VPC A → 10.0.0.0/16 VPC B → 10.1.0.0/16

### Q15. Your application is running in only one Availability Zone, and that AZ experiences an outage. The application becomes unavailable. What was the architectural problem? 

**Answer:**  The application had a single-AZ dependency. For a highly available architecture, I would deploy application resources across multiple Availability Zones and use an appropriate traffic-distribution mechanism.

### Q16. An application is experiencing high CPU utilization, while memory usage is normal. How would you approach the EC2 capacity problem? 

**Answer:**  I would first confirm that CPU is actually the bottleneck. If the workload requires more CPU capacity, I could consider moving to an EC2 instance type with more appropriate compute capacity. Depending on the workload, horizontal scaling may also be preferable to simply increasing the size of one instance.

### Q17. An application has low traffic most of the day but extremely high traffic during business hours. How could you optimize the infrastructure? 

**Answer:**  I would consider an elastic scaling strategy. For example, an Auto Scaling Group can adjust EC2 capacity based on demand. This can provide more capacity during peak periods while reducing unnecessary resources during low-demand periods.

### Q18. An EC2 instance is accidentally terminated. The company needs to rebuild the server quickly. What would you have prepared beforehand? 

**Answer:**  I would prepare appropriate backups and recovery mechanisms, such as: ● AMIs ● EBS snapshots ● AWS Backup where appropriate ● Automated backup schedules ● Documented recovery procedures An AMI can help recreate an EC2 server configuration quickly, while application data may require separate protection.

### Q19. The business requires an RTO of 15 minutes, but the current recovery process takes two hours. What should the team do? 

**Answer:**  The current disaster recovery strategy does not meet the required RTO. The team should redesign and test the recovery process to reduce recovery time. Depending on business requirements, this could involve automation, preconfigured infrastructure, faster restoration mechanisms, or a different disaster recovery architecture.

### Q20. The business can tolerate only 10 minutes of data loss, but backups run once every 24 hours. What is the problem? 

**Answer:**  The backup frequency does not satisfy the required RPO of 10 minutes. A failure could result in significantly more than 10 minutes of data loss. The organization needs a backup or replication strategy that aligns with the required RPO.

### Q21. A company has backups, but during a disaster the team discovers that the application cannot be restored because the required configuration is missing. What does this tell you? 

**Answer:**  It shows that having backups does not automatically mean the organization has a complete disaster recovery solution. The recovery plan should consider: ● Data ● Infrastructure ● Application configuration ● Networking ● Security ● Dependencies ● Recovery procedures The recovery process should also be tested regularly.

### Q22. An administrator claims they did not terminate an EC2 instance, but the instance was terminated. How could you investigate? 

**Answer:**  I would check AWS CloudTrail for the relevant API event.I would investigate: ● Identity ● Timestamp ● API operation ● Source IP ● User agent ● Region ● Credentials or role involved CloudTrail can provide valuable evidence about who performed AWS API actions.

### Q23. A developer can view EC2 instances but cannot terminate them. What is the likely cause? 

**Answer:**  The developer's IAM permissions may allow actions such as describing EC2 instances but not terminating them. I would inspect the IAM policies attached to the relevant user or role. For example, the identity may have permission for: ec2:DescribeInstances but not: ec2:TerminateInstances

### Q24. Developers need to manage EC2 instances, but security policy says they must not modify IAM. How would you implement this? 

**Answer:**  I would create an IAM policy or role that grants only the required EC2 permissions. For example, developers may be allowed to: ● Describe instances ● Start instances ● Stop instances ● Reboot instances but not modify IAM users, roles, or policies.This follows the principle of least privilege.

### Q25. An organization wants to know who changed an AWS resource, what was changed, and when it happened. Which service would you use, and how would you investigate? 

**Answer:**  I would use AWS CloudTrail.I would search the relevant events and examine: ● Event name ● User/role identity ● Timestamp ● Resource involved ● Source IP ● Request details ● Region This allows the organization to investigate AWS API activity and establish an audit trail.
