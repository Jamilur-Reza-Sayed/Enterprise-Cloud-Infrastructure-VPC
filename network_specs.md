# Network Specifications: Secure 3-Tier Architecture

## 1. VPC Configuration
* **Region:** AP-Hong Kong (Example)
* **VPC CIDR:** `10.0.0.0/16`
* **Availability Zones:** 2 (for High Availability)

## 2. Subnet Segmentation
| Subnet Name | CIDR Block | Type | Purpose |
| :--- | :--- | :--- | :--- |
| **Public-Subnet-01** | `10.0.1.0/24` | Public | Hosts ELB and NAT Gateway |
| **App-Private-01** | `10.0.2.0/24` | Private | Hosts Application Servers (ECS) |
| **DB-Private-01** | `10.0.3.0/24` | Private | Hosts Database (RDS/GeminiDB) |

## 3. Security Group Rules (Firewall)

### SG_Load_Balancer (Public)
* **Inbound:** Port 443 (HTTPS) from `0.0.0.0/0`
* **Outbound:** Port 80 to `SG_App_Server`

### SG_App_Server (Private)
* **Inbound:** Port 80 from `SG_Load_Balancer`
* **Inbound:** Port 22 (SSH) from `Admin_IP_Only`
* **Outbound:** Port 3306 to `SG_Database`

### SG_Database (Isolated)
* **Inbound:** Port 3306 from `SG_App_Server`
* **Outbound:** None (Strict Isolation)

docs: define network architecture and security rules
