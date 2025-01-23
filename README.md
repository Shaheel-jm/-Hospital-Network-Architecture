# Network-Architecture-and-Design-for-The-Hospital
# Hospital Network Infrastructure Setup

This document outlines the network and system architecture for the hospital, including the deployment of key services, security measures, and hardware configuration.

## **System Overview**

The proposed network architecture is designed to provide a secure, efficient, and scalable infrastructure tailored for a hospital environment. It uses VLAN segmentation to optimize traffic and isolate critical resources, with dedicated networks for servers, staff, visiting doctors, and wireless access points. A pfSense firewall ensures secure external communication and mitigates threats.

As the network and system administrator, I managed the firewall and servers, implemented access control, safeguarded sensitive data, and monitored network traffic. The design includes centralized backup systems and Active Directory for data integrity and operational continuity, ensuring compliance with healthcare IT standards.

The architecture follows a hybrid design, hosting application services in the cloud while maintaining on-premises database storage for enhanced security and reliability.


## Network design
<p align="center">
  <img src="Network%20Design.png" width=75%>
</p>

___

## Network Segmentations
* Staff Network | VLAN 17 | Network : 192.168.17.0/24
* Visiting Doctor's Network | VLAN 27 | Network : 192.168.27.0/24
* Access Point Network | VLAN 47 | Network : 192.168.47.0/24
* Server Network | VLAN 37 | Network : 192.168.37.0/24

## Hardware & Software
### Swtich
  * Model : Cicso IOU

In the hospital network, managed switches with VLAN segmentation are used to optimize network performance and manage traffic efficiently. By dividing the network into separate VLANs for different departments or devices, the network can reduce congestion, improve bandwidth utilization and ensure smoother communication.

This segmentation isolates traffic, reducing disruptions and creating a more organized and reliable infrastructure. While not directly focused on security, VLANs help prioritize critical traffic and prevent bottlenecks, making the network more efficient and better suited for the hospital's operational needs.

### Servers
* Operatiting System: Windows Server 2019
  * User Management: Managed through the Active Directory Domain Controller, this service handles the authentication and authorization of users, ensuring centralized management of user accounts, permissions, and policies across the network.

  * Database: Managed by SQL Server, this server is responsible for hosting the hospital's critical databases, ensuring that the data is stored securely and efficiently, and providing fast access for authorized users.

  * Backup: Handled by Veeam backup software, this service ensures the hospital's data is regularly backed up and can be restored in case of a failure or disaster, providing an additional layer of data security and business continuity.

Each service is running on a separate hardware instance to ensure optimal performance, reliability, and security.

### Firewall
  * **pfSense** is deployed to manage network traffic and ensure security across the internal and external communications.

___

## Firewall Configuration Goals
1. Traffic Isolation

To keep hospital network traffic separate from the wireless access point (AP) traffic, we can use VLANs to create separate networks for each. This ensures that traffic from the hospital’s internal network doesn't mix with traffic from the visitors or patients using the Wi-Fi. The pfSense firewall helps control this separation by blocking unnecessary communication between the networks. The Wi-Fi for visitors and patients is set up on its own network, keeping the hospital's systems secure and running smoothly.

#### Steps to isolate traffic: in this scenario traffic from wifi network has to isolated from internal LAN network.
- By leveraging Rules in the pfSense firewall, we can easily isolate traffic by selecting the respective interface, setting the action to Block, and specifying the destination as the network that should be isolated from the respective interface.
- Since there are multiple VLAN networks in the respective infrastructure, I am grouping all internal network using `Aliases`.
<p align="center">
  <img src="" width=49%>
  <img src="" width=49%>
</p>

___
