# Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines

This tutorial demonstrates how to observe network traffic between Azure Virtual Machines using Wireshark and how to control traffic using Network Security Groups (NSGs).

## Environments and Technologies Used

* Microsoft Azure (Virtual Machines)
* Remote Desktop
* Various Command-Line Tools
* Various Network Protocols (SSH, RDP, DNS, HTTP/S, ICMP, DHCP)
* Wireshark (Protocol Analyzer)

## Operating Systems Used

* Windows 10 (21H2)
* Ubuntu Server 20.04

## High-Level Overview

1.  Create Resources
2.  Observe ICMP Traffic
3.  Observe SSH Traffic
4.  Observe DHCP Traffic
5.  Observe DNS Traffic
6.  Observe RDP Traffic

## Actions and Steps

1.  **VM Creation and Setup:**
    * Create two Azure VMs in the same VNET: one Windows 10 VM and one Ubuntu Server 20.04 VM, each with two CPUs.
    * On the Windows 10 VM, download and install Wireshark.
    * [Screenshot 1 - Azure VM Creation]
![img1](https://github.com/user-attachments/assets/02c77055-5cb1-4d75-ba78-c49076bed4ed)

2.  **Observing ICMP Traffic:**
    * In Wireshark, filter for ICMP traffic.
    * From the Windows 10 VM, ping the private IP address of the Ubuntu VM.
    * Observe the ICMP packets in Wireshark.
![img2](https://github.com/user-attachments/assets/4d977dae-602f-40a8-b299-7643241c4662)

    * Attempt to ping google.com and observe results.
    * Initiate a perpetual ping from the Windows 10 VM to the Ubuntu VM.
    * Create a new Network Security Group (NSG) for the Ubuntu VM and block inbound ICMP traffic.
    * Observe the lack of ICMP echo replies in Wireshark.
    * Enable inbound ICMP traffic in the Ubuntu VM's NSG.
![img3](https://github.com/user-attachments/assets/8ffdcc24-ba05-491a-bea9-adf0dd2d6d90)

3.  **Observing SSH Traffic:**
    * In Wireshark, filter for SSH traffic.
    * From the Windows 10 VM, SSH into the Ubuntu VM using its private IP address.
    * Execute commands (e.g., `ls`, `pwd`) in the SSH session.
    * Observe the SSH traffic in Wireshark.
    * Exit the SSH session.

4.  **Observing DHCP Traffic:**
    * In Wireshark, filter for DHCP traffic.
    * From the Windows 10 VM, use `ipconfig /renew` to request a new IP address.
    * Observe the DHCP traffic in Wireshark.
![dhcp traff](https://github.com/user-attachments/assets/25789281-2ad7-474c-9cf4-b5feaf1aac32)

5.  **Observing DNS Traffic:**
    * From the Windows 10 VM, use `nslookup` to resolve `google.com` and `disney.com`.
    * Observe the DNS traffic in Wireshark.
![dns traff](https://github.com/user-attachments/assets/5e822062-f1a8-48a7-a154-c1bf57c49c3c)

6.  **Observing RDP Traffic:**
    * In Wireshark, filter for RDP traffic using `tcp.port == 3389`.
    * Observe RDP traffic during a RDP session.
![rdp traffic](https://github.com/user-attachments/assets/f3040b20-c1d5-478a-a25a-d9ed8877c0a4)

7.  **Cleanup:**
    * Close the Remote Desktop connection.
    * Delete the Azure Resource Group(s) created for this tutorial.
    * Verify the Resource Group deletion.
