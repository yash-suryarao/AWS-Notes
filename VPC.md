
#Amazon Virtual Private Cloud (VPC)

-AWS VPC allows you to provision a logically isolated section of the AWS cloud where you can launch AWS resources in a virtual network that you define. It provides control over your network settings, such as IP address ranges, subnets, route tables, and gateways, to build a secure and scalable environment for your applications.

#components of vpc

1.CIDR Block

- When you create a VPC, you specify a CIDR block (Classless Inter-Domain Routing) for the VPC's IP address range (e.g., 10.0.0.0/16). 
- This range determines the total number of IP addresses available for your VPC.

2.Subnets

Subnets are subdivisions of a VPC's IP address range within which you place your AWS resources (e.g., EC2 instances, RDS databases).
- Types of Subnets:
  - Public Subnets: Have a route to an Internet Gateway (IGW) and can access the internet directly.
  - Private Subnets: Do not have a route to an IGW and are isolated from the internet.
  - VPN-Only Subnets: Have a route to a Virtual Private Gateway (VGW), enabling connectivity to on-premises networks via VPN.

3. Route Tables

 Route tables control the routing for traffic within the VPC and between VPCs or between VPCs and external networks.
Types of Route Tables:
  - Main Route Table:Automatically created for each VPC; controls the routing for all subnets unless explicitly associated with a custom route table.
  - Custom Route Tables:You can create additional route tables to customize routing for specific subnets.

4. Internet Gateway (IGW)
 -An IGW is a horizontally scaled, redundant, and highly available VPC component that allows communication between instances in your VPC and the internet.
- You must attach an IGW to your VPC and update the associated route tables to route internet-bound traffic through the IGW.

5.NAT Gateway and NAT Instances

- NAT Gateway: A managed service that enables instances in private subnets to connect to the internet or other AWS services but prevents inbound traffic initiated by the internet.
- NAT Instance:An EC2 instance configured to perform network address translation (NAT). NAT instances require manual configuration and management.

6.Security Groups

- Definition: Security Groups act as a virtual firewall for your instances to control inbound and outbound traffic.
- Stateful:Return traffic is automatically allowed, regardless of any rules.
- Rule Configuration: You define allow rules (ingress) and outbound rules (egress) based on protocols, ports, and IP ranges.

 7.Network Access Control Lists (NACLs)

- Definition:NACLs are an optional layer of security for your VPC that act as stateless firewalls at the subnet level.
- Stateless:Inbound and outbound rules must be explicitly configured.
- Order of Evaluation: Rules are evaluated in numerical order, starting with the lowest number.

8.VPC Peering

- Definition:VPC Peering allows you to connect two VPCs and route traffic between them using private IP addresses as if they were on the same network.
- Transitive Peering: Direct peering connections do not support transitive peering through a third VPC.

9. VPN Connections and AWS Direct Connect

- VPN Connections: Secure connections between your on-premises networks and your VPCs using virtual private gateways (VGWs) and customer gateways.
- AWS Direct Connect: Dedicated network connection from your premises to AWS, providing private connectivity without traversing the internet.

10. Elastic IP Addresses (EIPs)

-EIPs are static IPv4 addresses designed for dynamic cloud computing. They remain associated with your AWS account until released.

11. Endpoints

- Gateway Endpoints:Enable private connectivity between your VPC and supported AWS services (e.g., S3, DynamoDB) without requiring an internet gateway or NAT device.
- Interface Endpoints: Used for AWS PrivateLink to connect to AWS services privately through a network interface.

12. Flow Logs

- Definition: Flow Logs capture information about IP traffic going to and from network interfaces in your VPC.
- Uses: Troubleshoot connectivity issues, monitor traffic patterns, and analyze security threats.


#VPC Limits

| Component                     | Default Limit |
|-------------------------------|---------------|
| VPC                           | 5 per Region  |
| Subnets                       | 200 per VPC   |
| Route Tables                  | 200 per VPC   |
| Internet Gateway              | 5 per VPC     |
| NAT Gateway                   | 5 per AZ      |
| Virtual Private Gateway       | 5 per Region  |
| Customer Gateway              | 50 per Region |
| VPC Peering Connection        | 50 per VPC    |
| Security Groups               | 2,500 per VPC |
| Network ACLs                  | 200 per VPC   |
| Elastic IP Addresses          | 5 per Region  |
| DHCP Option Sets              | 10 per Region |
| Egress-Only Internet Gateway  | 5 per VPC     |
| Transit Gateway               | 5 per Region  |

