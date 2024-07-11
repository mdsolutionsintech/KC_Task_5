# 1: Create a VPC
Open the VPC Console:
Create a VPC:
Click Create VPC.
Name: KCVPC
IPv4 CIDR block: 10.0.0.0/16
Click Create VPC.
## 2: Create Subnets
Create a Public Subnet:
Click on "Subnets" in the left-hand menu.
Click Create Subnet.
VPC: Choose KCVPC
Name: PublicSubnet
IPv4 CIDR block: 10.0.1.0/24
AZ: choose any
Click Create.
Create Private Subnet:
Again, click Create Subnet.
VPC: Choose KCVPC
Name: PrivateSubnet
IPv4 CIDR block: 10.0.2.0/24
AZ: do as Public Subnet 
Click Create.

## 3: Configuring Internet Gateway (IGW)
Creating and Attaching an IGW:
Click on Internet Gateways.
Click Create internet gateway.
Name: KCVPC-IGW
Click Create.
Select the created IGW, click Actions and Attach to VPC.
VPC: Select KCVPC
Click Attach.

## 4: Route Tables Configuring
Create a Public Route Table:
Click on Route Tables.
Click Create route table.
Name: PublicRouteTable
VPC: Select KCVPC
Click Create.
Add Route to IGW:
Select PublicRouteTable, click Routes tab and Edit routes.
Click Add route.
Destination: 0.0.0.0/0
Target: Select the IGW (KCVPC-IGW)
Click Save routes.
Associate Public Subnet with Public Route Table:
Click Subnet Associations tab and Edit subnet associations.
Select PublicSubnet
Click Save.
Create a Private Route Table:
Click Create route table.
Name: PrivateRouteTable
VPC: Select KCVPC
Click Create.
Associate Private Subnet with Private Route Table:
Select PrivateRouteTable, click Subnet Associations tab and Edit subnet associations.
Select PrivateSubnet
Click Save.

## 5: Set up NAT Gateway
Create a NAT Gateway:
Click on NAT Gateways.
Click Create NAT gateway.
Subnet: Select PublicSubnet
Allocate Elastic IP: Click Allocate Elastic IP and select it.
Click Create.
Update Private Route Table:
Select PrivateRouteTable, click Routes tab and Edit routes.
Click Add route.
Destination: 0.0.0.0/0
Target: Select the NAT Gateway
Click Save routes.

## 6: Security Groups
Create Public Security Group:
Open the EC2 console.
click Security Groups.
Click Create security group.
Name: PublicSG
VPC: KCVPC
Add inbound rules to allow HTTP (80), HTTPS (443), and SSH (22) from 0.0.0.0/0.
Add outbound rule to allow all traffic.
Click Create.
Create Private Security Group:
Click Create security group.
Name: PrivateSG
VPC: Select KCVPC
Add inbound rule for MySQL (3306) from PublicSubnet.
Add outbound rule to allow all traffic.
Click Create.

## 7: Configure Network ACLs
Create Public Subnet NACL:
Click on Network ACLs in the VPC console.
Click "Create network ACL".
Name: PublicSubnetNACL
VPC: Select KCVPC
Click Create.
Select the NACL, click "Inbound Rules" tab, then "Edit inbound rules".
Add rules for HTTP (80), HTTPS (443), and SSH (22) from 0.0.0.0/0.
Click Save.
In the Outbound Rules tab, click on Edit outbound rules.
Add a rule to allow all traffic (0.0.0.0/0).
Click Save.
Associate it with PublicSubnet.
Create Private Subnet NACL:
Click "Create network ACL".
Name: PrivateSubnetNACL
VPC: Choose KCVPC
Click Create.
Add inbound rules to allow traffic from PublicSubnet.
Add outbound rules to allow traffic to PublicSubnet and the internet.
Associate to PrivateSubnet.

## 8: Deploy Instances
Launch Public Instance:
Open the EC2 console.
Click Launch Instance.
Configure instance details; select PublicSubnet and assign PublicSG.
Complete the launch and verify access via the internet.
Launch Private Instance:
Click Launch Instance.
Configure instance details; select PrivateSubnet and assign PrivateSG.
Complete the launch and verify access through the NAT Gateway and communication with the public instance.

![26](https://github.com/mdsolutionsintech/KC_Task_5/assets/170469142/d97cf63e-639b-4b6f-98df-2dbabf509aaf)
![25](https://github.com/mdsolutionsintech/KC_Task_5/assets/170469142/db59f72b-f6c0-412d-905d-8a8eb87397ad)
![24](https://github.com/mdsolutionsintech/KC_Task_5/assets/170469142/ce3ff18c-a505-4438-900d-374fab0b45f4)
![23](https://github.com/mdsolutionsintech/KC_Task_5/assets/170469142/8948fd92-cf13-4c16-8b4b-00ddff09715e)
![22](https://github.com/mdsolutionsintech/KC_Task_5/assets/170469142/6ef2ba00-d551-45bc-953d-269349dcaacf)
![21](https://github.com/mdsolutionsintech/KC_Task_5/assets/170469142/46503517-e3d7-4e7d-8a25-50ffb70d122a)
![20](https://github.com/mdsolutionsintech/KC_Task_5/assets/170469142/af152637-6810-48dc-9c36-6639367635d6)
![19](https://github.com/mdsolutionsintech/KC_Task_5/assets/170469142/85fdc7d9-eec4-4b0f-af3d-e9a98cb06ca8)
![18](https://github.com/mdsolutionsintech/KC_Task_5/assets/170469142/0d6f7126-871c-4ea0-8e67-bff90430eace)
![17](https://github.com/mdsolutionsintech/KC_Task_5/assets/170469142/04365d24-62c2-403c-8eac-fa0847b3778b)
![16](https://github.com/mdsolutionsintech/KC_Task_5/assets/170469142/51559f08-b22b-48c7-a6ce-b43cc58e274f)
![15](https://github.com/mdsolutionsintech/KC_Task_5/assets/170469142/1237e273-f5b4-499d-a122-28da00e09295)
![14](https://github.com/mdsolutionsintech/KC_Task_5/assets/170469142/4e1bafad-034a-4edf-881b-7e26debeaec3)
![13](https://github.com/mdsolutionsintech/KC_Task_5/assets/170469142/aa07c559-d00a-4a91-9bf7-f69ecaeb7243)
![12](https://github.com/mdsolutionsintech/KC_Task_5/assets/170469142/4eaa2402-31fe-4631-aaa7-e0484290ea1f)
![11](https://github.com/mdsolutionsintech/KC_Task_5/assets/170469142/efa7ffca-bef7-4d90-bec4-ddbe7ac381d5)
![10](https://github.com/mdsolutionsintech/KC_Task_5/assets/170469142/39a5145c-32d0-48e9-8b36-2d07a8270da3)
![9](https://github.com/mdsolutionsintech/KC_Task_5/assets/170469142/c04b65eb-754d-4142-8185-c3b61d70bf05)
![8](https://github.com/mdsolutionsintech/KC_Task_5/assets/170469142/2d045487-0e19-4066-b8cc-38d12edb5352)
![7](https://github.com/mdsolutionsintech/KC_Task_5/assets/170469142/7759a6dd-16ef-4a55-91a1-31f147a1f703)
![6](https://github.com/mdsolutionsintech/KC_Task_5/assets/170469142/69558a0e-3718-463f-91c2-f38a3f9f4985)
![5](https://github.com/mdsolutionsintech/KC_Task_5/assets/170469142/c4ab9bb5-44b0-4007-8e8a-9751010ee5de)
![4](https://github.com/mdsolutionsintech/KC_Task_5/assets/170469142/85d19a2b-a41c-465c-8897-455a02b7eda4)
![3](https://github.com/mdsolutionsintech/KC_Task_5/assets/170469142/6a6be812-5b74-405e-b1c8-5f0fc7809c59)
![2](https://github.com/mdsolutionsintech/KC_Task_5/assets/170469142/8d08d198-9984-4836-bfa0-c4f7800754e2)
![1](https://github.com/mdsolutionsintech/KC_Task_5/assets/170469142/0fd1c7cd-eb65-4286-a142-258e85b70ec9)
![26a](https://github.com/mdsolutionsintech/KC_Task_5/assets/170469142/5efeadab-37e3-4115-a215-abf8af31669f)
