

**Title:**  
**Comprehensive Cisco Network Configuration: VLANs, Trunking, and Inter-VLAN Routing**

**Description:**  
This project demonstrates the step-by-step configuration of a Cisco switch and router to implement **VLANs**, **trunking**, and **inter-VLAN routing**. By configuring two VLANs (VLAN 10 and VLAN 20), trunk links, and router subinterfaces, this setup enables seamless communication across isolated networks. It’s designed to simulate a small business or enterprise network where different departments (represented by the VLANs) need to communicate across multiple segments, with routing provided through a central router. Whether you’re a beginner or an intermediate learner, this project provides hands-on experience with essential networking concepts in Cisco environments.

This title and description are designed to be more professional and informative while clearly explaining the scope and purpose of the project.

Welcome to the **Network Configuration Project**, where we dive deep into the world of **Cisco switching** and **routing**. This repository showcases the detailed configuration of a **Cisco switch** and **router**, utilizing **VLANs**, **trunking**, and **inter-VLAN routing**. This project simulates a network with two VLANs (VLAN 10 and VLAN 20), connected to the switch and configured for communication between VLANs via a router.

---

## 🌟 Project Overview

In this project, we will guide you through the process of:

- Setting up **VLANs** on a Cisco switch.
- Configuring **trunking** for multi-VLAN communication.
- Enabling **inter-VLAN routing** on a Cisco router.

This configuration simulates a **small network environment** where **departmental communication** across different VLANs (10 & 20) is essential. By the end of this, you'll understand how to connect multiple VLANs and enable seamless communication.

---

## 🖧 Switch Configuration

The **switch configuration** involves creating VLANs, configuring trunking, and assigning ports to VLANs for access or trunking.

### ⚙️ VLAN Setup

VLANs represent the segmentation of your network into **logical subnets**. Here's how we create and configure them:

- **VLAN 10** - Representing **Department AA**.
- **VLAN 20** - Representing **Department BB**.
- **VLAN 99** - The **native VLAN** for trunking.

**Configuration Commands:**
```bash
Switch(config)# vlan 10
Switch(config-vlan)# name AA
Switch(config-vlan)# exit

Switch(config)# vlan 20
Switch(config-vlan)# name BB
Switch(config-vlan)# exit

Switch(config)# vlan 99
Switch(config-vlan)# name native
Switch(config-vlan)# exit
```

### 🔗 Trunking and Access Ports

To allow VLAN traffic to flow between devices, we configure **access** and **trunk ports**:

- **Access Ports**: Assigned to specific VLANs (VLAN 10 and VLAN 20).
- **Trunk Ports**: Carry multiple VLAN traffic and allow communication between switches.

**Configuration Commands:**
```bash
Switch(config)# int range fa0/1-2
Switch(config-if-range)# switchport mode access
Switch(config-if-range)# switchport access vlan 10
Switch(config-if-range)# exit

Switch(config)# int range fa0/3-4
Switch(config-if-range)# switchport mode access
Switch(config-if-range)# switchport access vlan 20
Switch(config-if-range)# exit

Switch(config)# int fa0/23
Switch(config-if)# switchport mode trunk
Switch(config-if)# switchport trunk native vlan 99
Switch(config-if)# switchport trunk allowed vlan 10,20
Switch(config-if)# exit

Switch(config)# int fa0/24
Switch(config-if)# switchport mode trunk
Switch(config-if)# exit
```

---

## 🖥️ Router Configuration

The router will enable **inter-VLAN routing**, allowing devices in different VLANs to communicate with each other.

### 🌐 Subinterfaces

Each VLAN is routed through a **subinterface** on the router, with each subinterface associated with its own **IP address**.

**Subinterface Configuration:**
- **GigabitEthernet0/0.10** - IP: `192.168.1.62` (VLAN 10).
- **GigabitEthernet0/0.20** - IP: `192.168.1.126` (VLAN 20).

**Router Configuration Commands:**
```bash
Router(config)# interface GigabitEthernet0/0.10
Router(config-if)# encapsulation dot1Q 10
Router(config-if)# ip address 192.168.1.62 255.255.255.192
Router(config-if)# exit

Router(config)# interface GigabitEthernet0/0.20
Router(config-if)# encapsulation dot1Q 20
Router(config-if)# ip address 192.168.1.126 255.255.255.192
Router(config-if)# exit
```
