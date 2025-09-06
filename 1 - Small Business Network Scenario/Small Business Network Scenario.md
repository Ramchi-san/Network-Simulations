# Scenario - Small Business Network Upgrade

**Company Profile**: "Summit Solutions," a 50-employee company has outgrown their simple flat network. They have three departments: 
- Engineering (VLAN 10),
- Sales (VLAN 20), and 
- Operations (VLAN 30).
They meed a secure, scalable design where departments are segmented but can access common resources like a file server and the internet.

## 1. Topology Design (The Collapsed Core)
This design merges the core and distribution layers into a single, powerful device. 
- **Core/Distribution Layer**: One Layer 3 Switch (e.g., Cisco 3650 or 3850 in Packet Tracer). This one device will be the heart of the network.
- **Access Layer**: Three Layer 2 Switches (e.g., Cisco 2960s), one for each department.
- **Other devices**:
    - 1x Router (e.g., 4321) for internet connectivity.
    - 1x Server (to act as both File Server and DHCP Server).
    - Multiple End Devices (PCs, printers) for each department.
- **Physical Connections**:
    - The L3 switch connects to each L2 Access Switch via a Gigabit Ethernet trunk link.
    - The L3 switch connects to the Router.
    - The Router connects to the Server and to an external "Cloud" or "ISP" object for the internet.

## 2. Key Configuration Tasks on the Layer 3 Switch (Your Focus)
This is where you simulate the "collapsed core" functionality. The L3 switch must be configured to handle both high-speed switching (core function) and intelligent routing (distribution function).

1. Inter-VLAN Routing
    - Create SVIs (Switched Virtual Interfaces) for each VLAN. These act as the default gateway for each department.
        - interface VLAN 10 | ip address 192.168.10.1 255.255.255.0
        - interface VLAN 20 | ip address 192.168.20.1 255.255.255.0
        - interface VLAN 30 | ip address 192.168.30.1 255.255.255.0
    - Enable IP routing on the switch: **ip routing**.

2. DHCP Relay
    -  Since your server is on another segment, you need to help DHCP requests find it.
    - On each SVI, set the ip helper-address to the IP of your DHCP server.
        - interface Vlan10 | ip helper-address 192.168.99.100

3. Trunking
    - 

# Studies brought on by the design
1. How to create an external cloud or ISP object?
2. How to configure with

access-list 1 permit 192.168.10.0 0.0.0.255
access-list 1 permit 192.168.20.0 0.0.0.255
access-list 1 permit 192.168.30.0 0.0.0.255
access-list 1 permit 192.168.100.0 0.0.0.255