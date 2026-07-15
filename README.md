VPC-Infrastructure
This project demonstrates the design and deployment of a secure AWS networking environment following AWS Well-Architected Framework principles

The infrastructure separates public-facing resources from private resources by implementing public and private subnets within a custom Virtual Private Cloud (VPC). Administrative access is securely controlled through a Bastion Host while private workloads access the internet through a NAT Gateway without being directly exposed.

Objectives

The primary objectives of this project were:

• Design production-ready AWS networking architecture  
• Understand core cloud isolation and security practices  
• Configure public and private subnets  
• Implement network routing and address translation (NAT)  
• Apply Network Access Control Lists (NACLs)  
• Align with the AWS Well-Architected Framework principles

AWS Services Used

Amazon VPC
Amazon EC2
Internet Gateway
NAT Gateway
Elastic IP
Route Tables
Security Groups
AWS Identity and Access Management (IAM)
AWS Console

Architecture

The environment consists of:

Internet
     │
Internet Gateway
     │
Public Route Table
     │
Public Subnet
     │
Bastion Host (EC2)
     │
SSH
     │
Private Subnet
     │
Private EC2
     │
Private Route Table
     │
NAT Gateway
     │
Internet

Network Configuration

Virtual Private Cloud
| Setting    | Value       |
| ---------- | ----------- |
| CIDR Block | 10.0.0.0/16 |

Public Subnet
| Setting   | Value   |
| -------   | ------- |
| Public IP | Enabled |

Private Subnet
| Setting   | Value   |
| -------   | ------- |
| Public IP | Disabled |

Security Groups: Bastion Host
Allowed inbound traffic:
| Protocol | Port | Source |
| -------- | ---- | ------ |
| SSH      | 22   | My IP  |

Private EC2

Allowed inbound traffic:
| Protocol | Port | Source                 |
| -------- | ---- | ---------------------- |
| SSH      | 22   | Bastion Security Group |

Route Tables:

Public Route Table:
| Destination | Target           |
| ----------- | ---------------- |
| 10.0.0.0/16 | Local            |
| 0.0.0.0/0   | Internet Gateway |

Private Route Table:
| Destination | Target      |
| ----------- | ----------- |
| 10.0.0.0/16 | Local       |
| 0.0.0.0/0   | NAT Gateway |

EC2 Instances
Bastion Host
Why we used the Bastion Host

-it Provides secure administrative access into the private network.

Characteristics:
Public IP Address
SSH Enabled
Located in Public Subnet


Private EC2
-Purpose:

it Hosts internal workloads without direct internet exposure.

Characteristics:
No Public IP
Accessible only through Bastion Host
Internet access via NAT Gateway

Connectivity Validation

The following connectivity tests were successfully completed:

SSH from Local Machine
Laptop
  |
  |
  |
Bastion Host

SSH FROM BASTION HOST

Bastion Host
    |
    |
    |
Private EC2


Internet Connectivity

Executed from the Private EC2:

I used ping amazon.com 
And curl https://aws.amazon.com

These tests confirmed that the Private EC2 accesses the internet securely through the NAT Gateway.








