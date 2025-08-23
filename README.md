# Cisco-Switch-Configuration
CLI Configuration Modes
The basic CLI modes that we will be referring to below are as follows:
Switch> <– User EXEC Mode (Default mode when you log in to the router CLI)
Switch#	<– Privileged EXEC mode (Enter <enable> to get into this mode)
Switch(config)#	<– Global Configuration Mode (enter <configure terminal> to switch to this mode)
Switch(config-if)# <– Interface Configuration Mode 
Switch(config-line)# <– Line Configuration Mode
ROMMON <-- Rom monitoring mode (enter <reload EXEC> command from privileged EXEC mode and click break during the first 60 seconds while the system is booting)

#Commands 
#Switch to the global config mode
STEP1
It is a very good security practice to lock down all access lines of a switch with a password. 
Set up a router password ----> enable secret <your password>

STEP2
Configure Hostname ----> hostname <your hostname>

STEP3 
(OPTIONAL) Configure a password for telnet and console access
It is a very good security practice to lock down all access lines of a switch with a password.
access-switch1(config)# line vty 0 15
access-switch1(config-line)# password <your password>
access-switch1(config-line)# login 
access-switch1(config-line)# exit 

access-switch1(config)# line console 0
access-switch1(config-line)# password <your password>
access-switch1(config-line)# login 
access-switch1(config-line)# exit 


STEP4
Define which IP addresses are allowed to access the switch via TELNET
access-switch1(config)# ip access-list standard TELNET-ACCESS 
access-switch1(config-std-nacl)# permit 10.1.1.100
access-switch1(config-std-nacl)# permit 10.1.1.101 
access-switch1(config-std-nacl)# exit

Apply the access list to Telnet VTY Lines
access-switch1(config)# line vty 0 15
access-switch1(config-line)# access-class TELNET-ACCESS in 
access-switch1(config-line)# exit

STEP5
Assign IP address to the switch for management
Management IP is assigned to Vlan 1 by default 
access-switch1(config)# interface vlan 1
access-switch1(config-if)# ip address 10.1.1.200 255.255.255.0 
access-switch1(config-if)# exit

STEP6
Assign the default gateway to the switch
access-switch1(config)# ip default-gateway 10.1.1.254

STEP7
Assign the default gateway to the switch
access-switch1(config)# ip default-gateway 10.1.1.254

STEP8 
Disable unneeded ports on the switch
This step is optional, but it enhances security
Assume that we have a 48-port switch and we don’t need ports 25 to 48 
access-switch1(config)# interface range fa 0/25-48
access-switch1(config-if-range)# shutdown 
access-switch1(config-if-range)# exit 

STEP9 
Configure Layer 2 VLANs and assign ports to them
By default, all physical ports of the switch belong to the native VLAN 1. One of the most important  functions of an Ethernet  switch  is  to segment the network into multiple Layer 2 VLANs (with each VLAN belonging to a different Layer 3 subnet).
To perform the above Layer 2 segmentation, you need to create additional VLANs from the default VLAN 1 and then assign physical ports to these new VLANs. Let’s create two new VLANs (VLAN2 and VLAN3) and assign two ports to each one.
1. First, create the Layer2 VLANs on the switch
access-switch1(config)# vlan 2
access-switch1(config-vlan)# name TEACHERS 
access-switch1(config-vlan)# exit

2. Now assign the physical ports to each VLAN. Ports 1-2 are assigned to VLAN2 and
ports 3-4 to VLAN3

access-switch1(config)# interface range fa 0/1-2
access-switch1(config-if-range)# switchport mode access 
access-switch1(config-if-range)# switchport access vlan 2 
access-switch1(config-if-range)# exit

STEP10
Save the configuration

Access-switch1(config)# exit
Access-switch1# wr













