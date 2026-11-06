# Cloud Lab 4 Submission — Amazon VPC

Copy this template to `cc-lab-YOUR_ID/lab4/README.md` in your own repository. Follow [the instructions](lab4-instruction.md). Put your screenshots in `lab4/images/` with the file names below.

- **Student name:** SARITH Seyla
- **Student ID:** e20221116
- **Learner Lab user name:** SARITH_SEYLA
- **Date completed:** 06/November/2026
---

## VPC and internet gateway

![lab4-vpc](images/01-vpc.png)

![Internet gateway attached](images/02-internet-gateway.png)

## Public subnet

![Public subnet](images/03-public-subnet.png)

![Public route table](images/04-public-route-table.png)

![EC2 instance in the public subnet](images/05-ec2-public.png)

![Internet test from the public subnet](images/06-test-public.png)

## Private subnet

![Private subnet](images/07-private-subnet.png)

![NAT gateway](images/08-nat-gateway.png)

![Private route table](images/09-private-route-table.png)

![EC2 instance in the private subnet](images/10-ec2-private.png)

![Internet test from the private subnet](images/11-test-private.png)

---

## Questions

1. The VPC is `10.0.0.0/24` and the subnets are `10.0.0.0/25` and `10.0.0.128/25`. How many IP addresses does each block contain, and why do the two subnets not overlap?
2. Both subnets are in the same VPC. What exactly makes `lab4-public-subnet` public and `lab4-private-subnet` private?
3. Why is the NAT gateway placed in the **public** subnet and not in the private one?
4. `lab4-ec2-02` has no public IP address. Can someone on the internet open a connection to it? Can it download updates? Explain both answers.
5. You tested internet access with Systems Manager instead of SSH. Why did the instances need `LabInstanceProfile` for this?

## Answers

1. `100.0.0.0/24`, there are 256 IPs
   `100.0.0.0/25`, there are 128 IPs
   `100.0.0.128/25`, there are 128 IPs
   The two subnets not overlap because one is for public instance and other one is for private instance, so the subnets need to be different.
2. `lab4-public-subnet` is public via setting auto assign IP address from VPC and the VPC is connected to Internet Gateway and `lab4-private-subnet` is private via unassign IP address from VPC, so it access the internet via Route Table and NAT.
3. Because it need to access the internet.
4. Yes, they can access to it. And can download updates. Because eventhough it's private but via the NAT and Route Table, it can be accessed from the internet.
5. Because SSM does not support and can't access without the Role, so we need to set the profile `LabInstanceProfile`. And this is free for our Lab but if we want to create a new one, we need to paid.



## Clean up

- [x] Instances terminated.
- [x] NAT gateway deleted and its Elastic IP released.
- [x] Internet gateway detached and deleted.
- [x] `lab4-vpc` deleted.