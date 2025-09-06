# Small-Medium Business Network 

## Edge Router

hostname Edge_Router

int g0/0/0
ip address 192.168.254.2 255.255.255.252
ip nat inside

int g0/0/1
ip address 203.0.113.10 255.255.255.252
ip nat outside

access-list 1 permit 192.168.10.0 0.0.0.255
access-list 1 permit 192.168.20.0 0.0.0.255
access-list 1 permit 192.168.30.0 0.0.0.255
access-list 1 permit 192.168.100.0 0.0.0.255

ip nat inside source list 1 interface GigabitEthernet0/0/1 overload

ip route 0.0.0.0 0.0.0.0 203.0.113.9

ip route 192.168.10.0 255.255.255.0 192.168.254.1 
ip route 192.168.20.0 255.255.255.0 192.168.254.1 
ip route 192.168.30.0 255.255.255.0 192.168.254.1 
ip route 192.168.100.0 255.255.255.0 192.168.254.1

## Core Multi-Layer Switch

hostname Core_Switch

ip routing

interface Vlan10
ip address 192.168.10.1 255.255.255.0
ip helper-address 192.168.100.2

interface Vlan20
ip address 192.168.20.1 255.255.255.0
ip helper-address 192.168.100.2

interface Vlan30
ip address 192.168.30.1 255.255.255.0
ip helper-address 192.168.100.2

interface Vlan100
description Server_VLAN
ip address 192.168.100.1 255.255.255.0

ip route 0.0.0.0 0.0.0.0 192.168.254.2 

interface range GigabitEthernet1/0/1-3
switchport trunk allowed vlan 10,20,30,100
switchport mode trunk

interface GigabitEthernet1/0/4
no switchport
ip address 192.168.254.1 255.255.255.252

interface GigabitEthernet1/0/5
switchport access vlan 100
switchport mode access


## DHCP Server 
**Note**:*The configuration here is for dhcp but isn't actually needed.*

Interface: Fast Ethernet 0
ip address: 192.168.100.2 255.255.255.0
default-gateway 192.168.100.1 
dns-server 8.8.8.8

ip dhcp excluded-address 192.168.10.1
ip dhcp excluded-address 192.168.20.1
ip dhcp excluded-address 192.168.30.1

ip dhcp pool Engineering_Pool
network 192.168.10.0 255.255.255.0
default-gateway 192.168.10.1 
dns-server 8.8.8.8

ip dhcp pool Sales_Pool
network 192.168.20.0 255.255.255.0
default-gateway 192.168.20.1 
dns-server 8.8.8.8

ip dhcp pool Operations_Pool
network 192.168.30.0 255.255.255.0
default-gateway 192.168.30.1 
dns-server 8.8.8.8


## Engineering Dept. Access Switch

vlan 10
name Engineering
vlan 20
name Sales
vlan 30
name Operations
vlan 100
name Server

int g0/1
switchport mode trunk
switchport trunk allowed vlan 10,20,30,100

int r fa0/1-24
switchport mode access
switchport access vlan 10

## Sales Dept. Access Switch
vlan 10
name Engineering
vlan 20
name Sales
vlan 30
name Operations
vlan 100
name Server

int g0/1
switchport mode trunk
switchport trunk allowed vlan 10,20,30,100

int r fa0/1-24
switchport mode access
switchport access vlan 20


## Operations Dept. Access Switch
vlan 10
name Engineering
vlan 20
name Sales
vlan 30
name Operations
vlan 100
name Server

int g0/1
switchport mode trunk
switchport trunk allowed vlan 10,20,30,100

int r fa0/1-24
switchport mode access
switchport access vlan 30



# ISP Router
int g0/0/0
ip address 209.0.113.9 255.255.255.252
no sh

ip route 0.0.0.0 0.0.0.0 209.0.113.10


