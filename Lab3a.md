# TNE10006 Cheat Sheet
![topo3a]()

## Configure 2 Switches and 2 hosts using VLAN and no trunk (Lab 3a)

**Connection Establishment**

``` 
S4(config)#vlan 99
S4(config-vlan)#name Management
S4(config-vlan)#int vlan 99
S4(config-if)#ip address 192.168.99.4 255.255.255.0
/// Initiate VLAN 99 and assign name, IP for it ///

S4(config-if)#vlan 10
S4(config-vlan)#name Users
S4(config-if)#int vlan 10
/// Initiate VLAN 10 and assign name for it ///

S4(config-vlan)#int range gi1/0/5-6
S4(config-if-range)#switchport mode access 
S4(config-if-range)#switchport mode access 
S4(config-if-range)#switchport access vlan 99
/// Assign port for VLAN and turn on its mode ///

S4(config-if-range)#int gi1/0/24 
S4(config-if)#switchport mode access
S4(config-if-range)#switchport access vlan 10
/// Assign port for VLAN and turn on its mode ///

//// DO THE SAME FOR OTHER SWITCH BUT CHANGE THE IP ////
```

After that assign IP and mask for end host to test configuration.


#### SSH and Security configurations (Lab 3a)

**SSH Configuration and User Authentication**

```
S4(config)#ip domain-name ccna.lab
S4(config)#crypto key generate rsa general-keys modulus 1024
S4(config)#username labuser privilege 15 secret labpassword
/// Set domain name, generate RSA key pair using 1024 bits and create user and its password ///

S4(config)#line vty 0 15 // Virtual Teletype of 16 allowing 16 SSH user connection //
S4(config-line)#transport input ssh // Only allow SSH //
S4(config-line)#login local // Use the local database (authentication stored on the switch) //
S4(config-line)#end
```

SSH connection to this Switch can be established using the following command
```
S3#ssh -l labuser 192.168.99.4
```

Additional configuration can also be added

```
S4(config)#ip ssh time-out 60
S4(config)#ip ssh authentication-retries 4
```

**Security Configuration**

- **Disable unused ports**
```
S4(config)#interface range gigabitEthernet 1/0/1 – 4
S4(config)#shutdown
```

- **Configure Switchport Port-security on Switch3**

```
S4(config)#switchport port-security                     
/// Enable switchport security ///

S4(config)#switchport port-security maximum N
/// Allow only N MAC address to be learned by this port ///

S4(config)#switchport port-security violation shutdown
/// Switch will shutdown if the restriction is violated ///

S4(config)#switchport port-security violation restrict
/// If the restriction is violated, packets with unknowm address will be dropped ///
/// The administrator will be notified by SNMP ///

S4(config)#switchport port-security violation protect
/// The same as restrict but no notification ///

S4(config)#switchport port-security mac-address sticky
/// Learned MAC address will not be flushed ///

S4(config)#switchport port-security mac-address xxxx.xxxx.xxxx
/// Manually allocatte a MAC address to the list of MAC addresses ///
```

These commands will show the related settings to ensure they have been enforced

```
S4(config)#show mac address-table 
S4(config)#show port-security
```