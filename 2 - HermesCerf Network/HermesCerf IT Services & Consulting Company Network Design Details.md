# HermesCerf IT Services & Consulting Company Design Details

The HermesCerf IT Service & Consulting is a medium-sized IT services and consulting firm. It operates a network supports departmental VLANs, dynamic routing with OSPF, and VLSM-based efficient IP addressing. The physical topology showcases redundant edge routers and the utilization of a collapsed core model, with the edge routers feeding into two core multilayer switches, and distributed via location-based division access switches per floor.

## Departments & Personnel

|           Department          | VLAN ID | Personnel |  Probable Additions | Subnet |  
|-------------------------------|:-------:|----------:|--------------------:|-------:|
| Engineering & IT Support      |    10   |     28    |         +22         |  /27   |   
| Sales & Marketing             |    20   |     16    |         +8          |  /28   |
| Operations / Service Delivery |    30   |     10    |         +10         |  /28   |
| Accounting & Payroll          |    40   |     8     |         +2          |  /29   |
| Human Resources               |    50   |     5     |         +5          |  /29   |
| Procurement                   |    60   |     5     |         +5          |  /29   |

|        Infrastructure         | VLAN ID | Subnet |  
|-------------------------------|:-------:|-------:|
| Servers                       |   100   |  /24   |   
| Network Management            |    99   |  /24   |
| Printers                      |    70   |  /24   |
| Wireless - Staff              |   200   |  /24   |
| Wireless - Guest              |   666   |  /24   |
| Voice                         |    88   |  /24   |


## Physical Topology
This showcases the placement and division of network devices on the premises of the HermesCerf building.

### 1st Floor
- **Engineering Wing**
    - 2 access switches used by Engineering & IT Support (48 ports - 8 Etherchannel trunks = 40 usable ports) | Access Switch 1-2
    - 2 printers
    - 2 IP phones
    - 2 access points
    - 28 PCs

- **Technical Operations Room**
    - an access switch used by Operations / Service delivery (24 ports - 4 Etherchannel trunks = 20 usable ports) | Access Switch 3
    - a printer
    - an IP phone
    - an access point
    - 10 PCs

- **Server Room**
    - 2 edge routers
    - 2 core switches
    - an access switch for servers | Access Switch 4
    - an access switch for guests | Access Switch 5
    - Multiple servers

- **Open Areas**
    - 2 access points for switches
    - Note: connect to access switch in server room


### 2nd Floor
- **Finance Room**
    - an access switch shared by Procurement and Accounting & Payroll (24 ports - 4 Etherchannel trunks = 20 usable ports) | Access Switch 6
    - 2 printers
    - 2 ip phones
    - an access point 
    - 13 PCs

- **Business Operations Room**
    - 2 access switches shared by Sales & Marketing and HR (48 ports - 8 Etherchannel trunks = 40 usable ports) | Access Switch 7 - 8
    - 2 printers
    - 2 IP phones
    - 2 access points
    - 21 PCs

- **Collaboration Zone**
    - an access point
    - Note: Connects to access switch in server room | Staff vlan

- **Open Areas**
    - 2 access points
    - Note: Connect to access switch in server room


## Logical Topology 
This showcases the connections and network address blocks utilized in these connections.

- **EdgeRouter1**
    - g0/0/0 -> ISP 
    - g0/0/1-2 -> CoreSwitch1
    - g0/1/0-1 -> CoreSwitch2 

- **EdgeRouter2**
    - g0/0/0 -> ISP
    - g0/0/1-2 -> CoreSwitch2
    - g0/1/0-1 -> CoreSwitch1

- **CoreSwitch1**
    - g1/0/1-2 -> EdgeRouter1
    - g1/0/3-4 -> EdgeRouter2
    - g1/0/5-6 -> CoreSwitch2
    - g1/0/7-8 -> AccessSwitch1
    - g1/0/9-10 -> AccessSwitch2
    - g1/0/11-12 -> AccessSwitch3
    - g1/0/13-14 -> AccessSwitch4
    - g1/0/15-16 -> AccessSwitch5
    - g1/0/17-18 -> AccessSwitch6
    - g1/0/19-20 -> AccessSwitch7
    - g1/0/21-22 -> AccessSwitch8

- **Core Switch 2**
    - g1/0/1-2 -> EdgeRouter2
    - g1/0/3-4 -> EdgeRouter1
    - g1/0/5-6 -> CoreSwitch1
    - g1/0/7-8 -> AccessSwitch1
    - g1/0/9-10 -> AccessSwitch2
    - g1/0/11-12 -> AccessSwitch3
    - g1/0/13-14 -> AccessSwitch4
    - g1/0/15-16 -> AccessSwitch5
    - g1/0/17-18 -> AccessSwitch6
    - g1/0/19-20 -> AccessSwitch7
    - g1/0/21-22 -> AccessSwitch8

- **Access Switch 1**
    - fa0/1-2 -> Core Switch 1
    - fa0/3-4 -> Core Switch 2
    - fa0/5-21 -> Access Ports for VLAN 10
    - fa0/22 -> EngrWingIPPhone1
    - fa0/23 -> EngrWingAccessPoint1
    - fa0/24 -> EngrWingPrinter1


- **Access Switch 2**
    - fa0/1-2 -> Core Switch 1
    - fa0/3-4 -> Core Switch 2
    - fa0/5-21 -> Access Ports for VLAN 10
    - fa0/22 -> EngrWingIPPhone2
    - fa0/23 -> EngrWingAccessPoint2
    - fa0/24 -> EngrWingPrinter2

- **Access Switch 3**
    - fa0/1-2 -> Core Switch 1
    - fa0/3-4 -> Core Switch 2
    - fa0/5-21 -> Access Ports for VLAN 30
    - fa0/22 -> TechOpRoomIPPhone
    - fa0/23 -> TechOpRoomAccessPoint
    - fa0/24 -> TechOpRoomPrinter

- **Access Switch 4**
    - fa0/1-2 -> Core Switch 1
    - fa0/3-4 -> Core Switch 2


- **Access Switch 5**
    - fa0/1-2 -> Core Switch 1
    - fa0/3-4 -> Core Switch 2

- **Access Switch 6**
    - fa0/1-2 -> Core Switch 1
    - fa0/3-4 -> Core Switch 2
    - fa0/5-13 -> Accounting & Payroll Access Port
    - 
    - fa0/14-20 -> Procurement Access Port
    - fa0/20-21 -> TechOpRoomIPPhone
    - fa0/22 -> TechOpRoomAccessPoint 
    - fa0/23-24 -> TechOpRoomPrinter


- **Access Switch 7**
    - fa0/1-2 -> Core Switch 1
    - fa0/3-4 -> Core Switch 2

- **Access Switch 8**
    - fa0/1-2 -> Core Switch 1
    - fa0/3-4 -> Core Switch 2



## Configurations

### EdgeRouter1
enable 
configure terminal
ipv6 unicast-routing

hostname EdgeRouter1
service password-encryption
security passwords min-length 10
enable secret ramcie12345
banner motd "Unauthorized access is strictly prohibited!"
login block-for 15 attempts 5 within 30

line con 0
logging synchronous
password ramcie12345
login 
exit

line vty 0 4
loggin synchronous
password ramcie12345
login
exit


### EdgeRouter2
enable 
configure terminal
ipv6 unicast-routing

hostname EdgeRouter2
service password-encryption
security passwords min-length 10
enable secret ramcie12345
login block-for 15 attempts 5 within 30
banner motd "Unauthorized access is strictly prohibited!"

line con 0
logging synchronous
password ramcie12345
login
exit

line vty 0 4
logging synchronous
password ramcie12345
login
exit


### CoreSwitch1
enable
configure terminal
hostname CoreSwitch1
service password-encryption
enable secret ramcie12345
banner motd "Unauthorized access is strictly prohibited!"

security passwords min-length 10 (not available)
login block-for 15 attempts 5 within 30

line con 0
logging synchronous
password ramcie12345
login
exit

line vty 0 4
logging synchronous
password ramcie12345
login
exit

ipv6 unicast-routing

### CoreSwitch2
enable
configure terminal
hostname CoreSwitch2
service password-encryption
enable secret ramcie12345
login block-for 15 attempts 5 within 30
banner motd "Unauthorized access is strictly prohibited!"

line con 0
logging synchronous
password ramcie12345
login 
exit

line vty 0 4
logging synchronous
password ramcie12345
login
exit


### AccessSwitch1
enable 
configure terminal
sdm prefer dual-ipv4-and-ipv6 default
end
reload

enable
Show sdm prefer
configure terminal
no ip domain lookup
hostname AccessSwitch1
service password-encryption
enable secret ramcie12345
banner motd "Unauthorized access is strictly prohibited!"

line con 0
logging synchronous
password ramcie12345
login
exit 

line vty 0 4
logging synchronous
password ramcie12345
login
exit

ipv6 unicast-routing

### AccessSwitch2
enable 
configure terminal
sdm prefer dual-ipv4-and-ipv6 default
end
reload

enable
Show sdm prefer
configure terminal
no ip domain lookup
hostname AccessSwitch2
service password-encryption
enable secret ramcie12345
banner motd "Unauthorized access is strictly prohibited!"

line con 0
logging synchronous 
password ramcie12345
login

line vty 0 4
loggin synchronous
password ramcie12345
login

ipv6 unicast-routing

### AccessSwitch3
enable 
configure terminal
sdm prefer dual-ipv4-and-ipv6 default
end
reload

enable
Show sdm prefer
configure terminal
no ip domain lookup
hostname AccessSwitch3
service password-encryption
enable secret ramcie12345
banner motd "Unauthorized access is strictly prohibited!"

line con 0
logging synchronous
password ramcie12345
login
exit

line vty 0 4
logging synchronous
password ramcie12345
login 
exit

ipv6 unicast-routing

### AccessSwitch4
enable 
configure terminal
sdm prefer dual-ipv4-and-ipv6 default
end
reload

enable
Show sdm prefer
configure terminal
no ip domain lookup
hostname AccessSwitch4
service password-encryption
enable secret ramcie12345
banner motd "Unauthorized access is strictly prohibited!"

line con 0
logging synchronous
password ramcie12345
login
exit

line vty 0 4
logging synchronous 
password ramcie12345
login
exit

ipv6 unicast-routing


### AccessSwitch5
enable 
configure terminal
sdm prefer dual-ipv4-and-ipv6 default
end
reload

enable
Show sdm prefer
configure terminal
no ip domain lookup
hostname AccessSwitch5
service password-encryption
enable secret ramcie12345
banner motd "Unauthorized access is strictly prohibited!"

line con 0
logging synchronous
password ramcie12345
login
exit

line vty 0 4
logging synchronous
password ramcie12345
login
exit

ipv6 unicast-routing



### AccessSwitch6
enable 
configure terminal
sdm prefer dual-ipv4-and-ipv6 default
end
reload

enable
Show sdm prefer
configure terminal
no ip domain lookup
hostname AccessSwitch6
service password-encryption
enable secret ramcie12345
banner motd "Unauthorized access is strictly prohibited!"

line con 0
logging synchronous 
password ramcie12345
login
exit

line vty 0 4
logging synchronous
password ramcie12345
login 
exit

### AccessSwitch7
enable 
configure terminal
sdm prefer dual-ipv4-and-ipv6 default
end
reload

enable
Show sdm prefer
configure terminal
no ip domain lookup
hostname AccessSwitch7
service password-encryption
enable secret ramcie12345
banner motd "Unauthorized access is strictly prohibited!"

ipv6 unicast-routing


### AccessSwitch8
enable 
configure terminal
sdm prefer dual-ipv4-and-ipv6 default
end
reload

enable
Show sdm prefer
configure terminal
no ip domain lookup
hostname AccessSwitch8
service password-encryption
enable secret ramcie12345
banner motd "Unauthorized access is strictly prohibited!"

Software Engineering | VLAN 10 | 10.10.10.0/24 |
IPv4 Addressing Scheme
    > Network Address: 10.10.10.0
    > Subnet Mask: 255.255.255.0 
    > Usable host range: 10.10.10.1 - 10.10.10.254
    > Broadcast address: 10.10.10.255
IPv6 Addressing Scheme:
    > 


Infrastructure | VLAN 20 | 10.10.20.0/24 |
IPv4 Addressing Scheme
    > Network Address: 10.10.20.0
    > Subnet Mask: 255.255.255.0
    > Usable host range: 10.10.20.1 - 10.10.10.254
    > Broadcast address: 10.10.20.255
IPv6 Addressing Scheme:
    > 


Technical Operations | VLAN 30 | 10.10.30.0/27 |
IPv4 Addressing Scheme
    > Network Address: 10.10.30.0
    > Subnet Mask: 255.255.255.224
    > Usable host range: 10.10.30.1 - 10.10.30.30
    > Broadcast address: 10.10.10.31
IPv6 Addressing Scheme:
    > 

Sales & Marketing | VLAN 40 | 10.10.40.0/26|
IPv4 Addressing Scheme
    > Network Address: 10.10.40.0
    > Subnet Mask: 255.255.255.192
    > Usable host range: 10.10.40.1 - 10.10.40.62
    > Broadcast address: 10.10.40.63
IPv6 Addressing Scheme:
    > 


Customer Agents | VLAN 50 | 10.10.50.0/24 | 
IPv4 Addressing Scheme
    > Network Address: 10.10.50.0
    > Subnet Mask: 255.255.255.0 or /24
    > Usable host range: 10.10.50.1 - 10.10.50.254
    > Broadcast address: 10.10.50.255
IPv6 Addressing Scheme:
    > 


Accounting & Payroll | VLAN 60 | 10.10.60.0/27 |
IPv4 Addressing Scheme
    > Network Address: 10.10.60.0
    > Subnet Mask: 255.255.255.224
    > Usable host range: 10.10.60.1 - 10.10.10.30
    > Broadcast address: 10.10.60.31
IPv6 Addressing Scheme:
    > 


Human Resources | VLAN 70 | 10.10.70.0/26 |
IPv4 Addressing Scheme
    > Network Address: 10.10.70.0
    > Subnet Mask: 255.255.255.192
    > Usable host range: 10.10.70.1 - 10.10.70.62
    > Broadcast address: 10.10.10.63
IPv6 Addressing Scheme:
    > 


Procurement | VLAN 80 | 10.10.80.0/27|
IPv4 Addressing Scheme
    > Network Address: 10.10.80.0
    > Subnet Mask: 255.255.255.192
    > Usable host range: 10.10.80.1 - 10.10.80.30
    > Broadcast address: 10.10.80.31
IPv6 Addressing Scheme:
    >  

Network Management| 90 | 10.10.90.0/24 |
IPv4 Addressing Scheme
    > Network Address: 10.10.90.0
    > Subnet Mask: 255.255.255.0
    > Usable host range: 10.10.90.1 - 10.10.90.254
    > Broadcast address: 10.10.90.255
IPv6 Addressing Scheme:
    > 


Servers | VLAN 100 | 10.10.100.0/24 |
IPv4 Addressing Scheme
    > Network Address: 10.10.100.0
    > Subnet Mask: 255.255.255.0
    > Usable host range: 10.10.100.1 - 10.10.100.254
    > Broadcast address: 10.10.100.255
IPv6 Addressing Scheme:
    > 


Printers | VLAN 110 | 10.10.110.0/24 | 
IPv4 Addressing Scheme
    > Network Address: 10.10.110.0
    > Subnet Mask: 255.255.255.0
    > Usable host range: 10.10.110.1 - 10.10.110.254
    > Broadcast address: 10.10.110.255
IPv6 Addressing Scheme:
    > 


Wireless | VLAN 120 | 10.10.120.0/24 |
IPv4 Addressing Scheme
    > Network Address: 10.10.120.0
    > Subnet Mask: 255.255.255.0
    > Usable host range: 10.10.120.1 - 10.10.120.254
    > Broadcast address: 10.10.120.255
IPv6 Addressing Scheme:
    > 

Voice | VLAN 130 | 10.10.130.0/24 |
