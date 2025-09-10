# HermesCerf IT Services & Consulting Company Design Details

The HermesCerf IT Service & Consulting is a medium-sized IT services and consulting firm that operates from a 2-floor office with almost a 100 employees.

The network supports departmental VLANs, dynamic routing with OSPF, and VLSM-based efficient IP addressing. The physical topology showcases redundant edge routers and the utilization of a collapsed core model, with the edge routers feeding into two core multilayer switches, and distributed via location-based division access switches per floor.

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
    - an access switch shared by Sales & Marketing and HR (48 ports - 8 Etherchannel trunks = 40 usable ports) | Access Switch 7 - 8
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

- **Access Switch 2**
    - fa0/1-2 -> Core Switch 1
    - fa0/3-4 -> Core Switch 2

- **Access Switch 3**
    - fa0/1-2 -> Core Switch 1
    - fa0/3-4 -> Core Switch 2

- **Access Switch 4**
    - fa0/1-2 -> Core Switch 1
    - fa0/3-4 -> Core Switch 2

- **Access Switch 5**
    - fa0/1-2 -> Core Switch 1
    - fa0/3-4 -> Core Switch 2

- **Access Switch 6**
    - fa0/1-2 -> Core Switch 1
    - fa0/3-4 -> Core Switch 2

- **Access Switch 7**
    - fa0/1-2 -> Core Switch 1
    - fa0/3-4 -> Core Switch 2

- **Access Switch 8**
    - fa0/1-2 -> Core Switch 1
    - fa0/3-4 -> Core Switch 2



