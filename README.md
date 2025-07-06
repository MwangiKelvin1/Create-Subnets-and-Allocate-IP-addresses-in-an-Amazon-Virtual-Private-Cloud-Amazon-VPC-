# Create Subnets and Allocate IP addresses in an Amazon Virtual Private Cloud (Amazon VPC)

## Lab Objectives
- Create a Virtual Private Cloud (VPC) with a custom IPv4 CIDR block to support 15,000 private IP addresses.

- Configure a public subnet within the VPC that allows at least 50 usable IP addresses.

- Use the AWS Management Console to set up the VPC and associated networking components (e.g., subnets, internet gateway).

- Apply subnetting principles to design and implement an IP addressing scheme that meets customer requirements.

---

## Scenario Overview

I received an email from a startup customer, Paulo Santos, who needed help setting up an Amazon Virtual Private Cloud (VPC). His requirements included:
- Approximately 15,000 private IP addresses for his internal systems
- At least 50 public IP addresses for his internet-facing operations

He also mentioned he preferred using a 192.x.x.x CIDR block but wasn’t sure which ones were private. My task was to guide him through the VPC setup, ensuring all requirements were met.

### This was his message.

Hello, Cloud Support!

I'm new to AWS, and I need help setting up a VPC. Can you please help me through the setup process? I would like to build only the VPC part and would like to make it look something like the following picture. Can you help me ensure  I have around 15,000 private IP addresses in this VPC available?  I would also like the VPC IPv4 CIDR block to be a 192.x.x.x. I don't remember which is a private range though. Can you confirm that? I would also like to allocate at least 50 IP addresses for the public subnet.

Thanks!
Paulo Santos
Startup Owner

---

#### Client Diagram

![alt text](<~Screenshot/1 the customer's VPC architecture.png>)

Figure: In the customer's VPC architecture, the customer needs approximately 15,000 IP addresses for their Seattle office headquarters and 50 IP addresses for their operations department, which will be in the public subnet.

---

## Tools & Technologies

- Amazon Web Services (AWS)
  - Amazon VPC
  - Subnetting
  - Route Tables
  - Internet Gateway

## Network Design

| Component        | Configuration             |
|------------------|---------------------------|
| VPC CIDR Block   | `192.168.0.0/18` (16,384 IPs) |
| Public Subnet    | `192.168.1.0/26` (64 IPs) |
| IPv6             | Disabled                  |
| VPC Name         | `First VPC`               |
| Subnet Name      | `Public subnet`           |

To determine the appropriate address ranges:
- I referred to [RFC 1918](https://datatracker.ietf.org/doc/html/rfc1918)
- I used [Subnet Calculator](https://www.subnet-calculator.com/cidr) or [Visual Subnet Calculator](https://www.davidc.net/sites/default/subnets/subnets.html) to ensure my CIDR blocks met the required address space


## Task 1: Investigate the customer's needs

Before you start, quickly go over what a VPC is:

- A Virtual Private Cloud (VPC) is a cloud-based, isolated network environment that functions like a traditional data center. It allows you to launch and manage AWS resources securely and quickly.

- Resources inside a VPC use private IP addresses to communicate internally. If an instance needs to connect to the internet, it must have a public IP address, and the VPC must include components like an internet gateway and a route table to enable that connectivity.

- A CIDR block (Classless Inter-Domain Routing) defines the IP address range of your VPC — for example, a /16 block includes over 65,000 addresses.

-A subnet is a segmented portion of the VPC’s IP address range. It helps organize and isolate resources within the VPC.

-To calculate subnet sizes and CIDR ranges, tools like Subnet Calculator(Mentioned above) are helpful.

-For selecting private IP address ranges, refer to the official guidelines in RFC 1918(Mention above), which outlines safe IP ranges for internal use.


For the client at Paulo Santos, you will build one VPC and a guide about how to launch one.

1. Logged in to the AWS Management Console
2. Searched and opened the **VPC** service
3. Launched the **CREATE VPC**
![alt text](<~Screenshot/2 Create vpc.png>)
Figure: Use the Create VPC button to launch a VPC.

4. Selected **"VPC with a Single Public Subnet"**
![alt text](<~Screenshot/3 CREATE VPC.png>)

5. Configured the following:
   - VPC CIDR block: `192.168.0.0/18`
   - Public Subnet CIDR: `192.168.1.0/26`
   - Named the VPC: `First VPC`
   - Subnet name: `Public subnet`
   - Left other settings as default

   ![alt text](<~Screenshot/4 AVAILABILITY ZONE.png>)

   ![alt text](<~Screenshot/6 Overview The Layout.png>)
6. Clicked **Create VPC**
![alt text](<~Screenshot/5 CREATE VPC.png>)
7. Verified successful creation in the **Your VPCs** section
![alt text](<~Screenshot/7 Create vpc workflow.png>)

---

## **Conclusion**

### Why Use Public and Private Subnets?

- **Public subnets** are for resources that must communicate with the internet (e.g., web servers). These use a **public IP** and are connected to an **Internet Gateway**.
- **Private subnets** are isolated from the internet — best for databases or internal services. To reach the internet, they need a **NAT gateway** (Will be covered in another lab).

## What I Learned

- How to calculate subnet sizes based on CIDR notation
- How to set up a basic VPC and public subnet in AWS
- How to apply RFC1918 standards in practical cloud environments
- The significance of public vs private IP address usage in cloud networks

## References

- [AWS VPC Documentation](https://docs.aws.amazon.com/vpc/)
- [RFC1918 – Private Address Space](https://datatracker.ietf.org/doc/html/rfc1918)
- [Subnet Calculator Tool](https://www.subnet-calculator.com/)
- [Visual Subnet Calculator](https://www.davidc.net/sites/default/subnets/subnets.html)

---

## Project Metadata

- **Project Type**: AWS Networking & Support  
- **Focus Area**: IP Address Management, EC2, VPC  
- **Role**: AWS Cloud Support Engineer  

### Author
**Kelvin Mwangi**  
Security Analyst | Network Security | Cloud Security  

- 🔗 **GitHub**: [MwangiKelvin1](https://github.com/MwangiKelvin1)  
- 🔗 **LinkedIn**: [linkedin.com/in/mwangikabuchu](https://linkedin.com/in/mwangikabuchu)  
- 🔗 **X (Twitter)**: [@MwangiKabuchu](https://twitter.com/MwangiKabuchu)  


---

