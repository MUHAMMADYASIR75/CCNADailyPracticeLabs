# CCNA-DAILY-LABS-

# CCNA Lab 01 – Basic Router Configuration, DHCP, and Remote Access

## 📌 Lab Title

**Basic Cisco Router Initial Configuration, DHCP Setup, and SSH Remote Management**

---

## 🎯 Lab Objective

The objective of this lab was to learn the basic configuration of a Cisco router, secure administrative access, configure network interfaces, enable SSH remote management, and provide automatic IP addressing to LAN users through DHCP.

---

# 🛠️ Devices Used

| Device                        | Quantity |
| ----------------------------- | -------- |
| Cisco 1841 Router             | 1        |
| Cisco Switch                  | 1        |
| PC                            | 1        |
| Copper Straight-Through Cable | 2        |

---

# 📊 Network Topology

```
          +------------+
          | Cisco 1841 |
          |    R1      |
          +------------+
                |
                |
          Fa0/0 |
                |
          +------------+
          |  Switch    |
          +------------+
                |
                |
          +------------+
          |    PC      |
          +------------+
```

---

# 🔹 Step 1: Add Network Devices

✔ Selected a **Cisco 1841 Router** from Packet Tracer.

✔ Added one **Switch** to the workspace.

✔ Added one **PC**.

✔ Connected all devices using **Copper Straight-Through Cables**.

### Connections

| Source Device | Interface       | Destination Device | Interface       |
| ------------- | --------------- | ------------------ | --------------- |
| Router R1     | FastEthernet0/0 | Switch             | FastEthernet0/1 |
| PC            | FastEthernet0   | Switch             | FastEthernet0/2 |

---

# 🔹 Step 2: Access Router CLI

✔ Opened the Router.

✔ Selected the **CLI (Command Line Interface)** tab.

✔ Entered privileged mode.

```bash
Router> enable
```

---

# 🔹 Step 3: Change Router Hostname

Changed the default hostname from Router to R1.

```bash
Router# configure terminal
Router(config)# hostname R1
```

### Result

```bash
R1(config)#
```

---

# 🔹 Step 4: Configure Enable Secret Password

Configured an encrypted password to secure privileged EXEC mode.

```bash
R1(config)# enable secret cisco123
```

### Purpose

🔹 Protects administrative access.

🔹 Encrypts the privileged mode password.

---

# 🔹 Step 5: Create Local Username and Password

Created a local user account for authentication.

```bash
R1(config)# username admin password admin123
```

### Purpose

✔ Used for SSH login.

✔ Provides secure user authentication.

---

# 🔹 Step 6: Configure Console Line Security

Configured password protection on the console port.

```bash
R1(config)# line console 0
R1(config-line)# password console123
R1(config-line)# login
R1(config-line)# exit
```

### Purpose

✔ Prevents unauthorized physical access to the router.

---

# 🔹 Step 7: Configure VTY Lines

Configured virtual terminal lines for remote access.

```bash
R1(config)# line vty 0 4
R1(config-line)# login local
R1(config-line)# transport input ssh
R1(config-line)# exit
```

### Purpose

✔ Allows remote login.

✔ Restricts access to SSH only.

✔ Uses local username database.

---

# 🔹 Step 8: Configure Domain Name

Configured a domain name required for SSH key generation.

```bash
R1(config)# ip domain-name ccna.local
```

---

# 🔹 Step 9: Generate RSA Keys for SSH

Generated RSA encryption keys.

```bash
R1(config)# crypto key generate rsa
```

Choose:

```bash
1024
```

### Purpose

✔ Enables SSH encryption.

✔ Secures remote management sessions.

---

# 🔹 Step 10: Enable SSH Version 2

Configured SSH Version 2.

```bash
R1(config)# ip ssh version 2
```

### Purpose

✔ More secure than SSH Version 1.

---

# 🔹 Step 11: Configure IP Address on FastEthernet0/0

Assigned an IP address to the router LAN interface.

```bash
R1(config)# interface fastethernet 0/0
R1(config-if)# ip address 192.168.1.1 255.255.255.0
R1(config-if)# no shutdown
R1(config-if)# exit
```

### Verification

```bash
R1# show ip interface brief
```

Expected Output:

```bash
Fa0/0     192.168.1.1     up     up
```

---

# 🔹 Step 12: Configure DHCP Service

Excluded the gateway address from DHCP assignment.

```bash
R1(config)# ip dhcp excluded-address 192.168.1.1
```

---

# 🔹 Step 13: Create DHCP Pool

Created a DHCP pool for LAN users.

```bash
R1(config)# ip dhcp pool LAN
R1(dhcp-config)# network 192.168.1.0 255.255.255.0
R1(dhcp-config)# default-router 192.168.1.1
R1(dhcp-config)# dns-server 8.8.8.8
R1(dhcp-config)# exit
```

### Purpose

✔ Automatically assigns IP addresses.

✔ Provides gateway information.

✔ Provides DNS configuration.

---

# 🔹 Step 14: Configure PC to Obtain IP Automatically

Opened:

```
PC → Desktop → IP Configuration
```

Selected:

```
DHCP
```

### Result

The PC automatically received:

```bash
IP Address     : 192.168.1.x
Subnet Mask    : 255.255.255.0
Default Gateway: 192.168.1.1
DNS Server     : 8.8.8.8
```

---

# 🔹 Step 15: Verify DHCP Operation

Used the following command:

```bash
R1# show ip dhcp binding
```

### Purpose

Displays leased IP addresses assigned to clients.

---

# 🔹 Step 16: Save Configuration

Saved the running configuration to NVRAM.

```bash
R1# copy running-config startup-config
```

---

# ✅ Skills Learned in Lab 01

✔ Cisco Router Initial Configuration

✔ Hostname Configuration

✔ Enable Secret Security

✔ Local User Creation

✔ Console Security

✔ VTY Line Configuration

✔ SSH Configuration

✔ RSA Key Generation

✔ Interface IP Addressing

✔ DHCP Configuration

✔ Network Connectivity

✔ Configuration Saving

---

# 📖 Lab Summary

In this first CCNA lab, a Cisco 1841 router, switch, and PC were deployed in Packet Tracer. The router was configured with a hostname, enable secret password, local user authentication, console and VTY security, and SSH remote access. An IP address was assigned to the FastEthernet0/0 interface, and a DHCP pool was created to dynamically provide IP addresses to LAN users. The connected PC successfully obtained network settings through DHCP, demonstrating proper communication between the router, switch, and end device. This lab provided foundational skills in Cisco router configuration, network security, IP addressing, DHCP services, and remote device management using SSH.
