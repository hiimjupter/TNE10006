
# STP - Spanning Tree Protocol



## Description:
STP stands for Spanning Tree Protocol, which is a network protocol used to prevent loops in a network topology.


### **Network Redundancy**
Redundancy is an essential part of network design. As modern networks are expected to run 24/7/365, even a short downtime can be disastrous for a business.
- Network redundancy implementation must be considered as much as possible at every point in the network so that if one network component fails, other component will take over with little or no downtime.

The following is an example of a poorly designed network
![Point of failure example](s)

The following is an example of a much better designed network
![Good network](sd)

> However, without STP, there is a problem that can destroy our redundant network.

### **Broadcast Storm**
![broadcast storm](as)

The Ethernet Frame has a TTL field to prevent infinite loops, however, Layer 2 does not have such a field. Therefore, these broadcast storm or the broadcast frames that loops indefinitely around the network will cause our network to be congested and eventually 'destroyed'.

### **Classic Spanning Tree Protocol or IEEE 802.1D**
Switches from ALL vendors run STP by default. It prevents Layer 2 loops by placing redundant ports in a blocking state, essentially disabling the interface. These interfaces then act as backups that can enter a forwarding state if an active interface fails.

Interfaces in a blocking state only send or receive STP messages or BPDUs (Bridge Protocol Data Unit)

Therefore by selecting which ports are **forwarding** or **blocking** STp creates a single path to/from each point in the network and prevent Layer 2 loop.

**THE PROCESS OF STP OCCURS AS FOLLOWS**

**1**. **Root Bridge** Election:
- **STP-enabled switches send/receive Hello BPDUs** out of all interface with the default timer of 2 seconds, if a switch receive a Hello BPDU on an interface, it knows that the interface is connected to another switch (Other devices do not use STP).
- Switches use one field in the STP BPDU, the **Bridge ID** to elect a root bridge for the network. **The switch with the lowest Bridge ID will win**, however, if the bridge priority is equal (it is set to 32768 by default), it will use the **MAC address as a tie-breaker**.
![Bridge ID](s)
- Cisco switches use a version of STP called PVST(Per-VLAN SPanning Tree). Therefore, there is a VLAN ID in the Bridge ID to enable different VLAN instances to forwarding or blocking state.

![Bridge Priority and Extended System ID]

As the **Bridge priority + Extended system ID** is a single field of the bridge ID and the extended system ID is set(by the VLAN ID) hence can not be changed, we can only change the STP bridge priory in units of 4096. That is:

```
0, 4096, 8192, 12288, 16384, 20480,.....
```
  **1.1** When a switch is powered on, it assumes it is the root bridge and send Hello BPDUs to all other bridge in the network.

  **1.2** Switches will only give up its position if it receives a 'superior' BPDU (with a lower bridge ID).

  **1.3** Once the topology has converged and all switches agree on the root bridge, only the root bridge sends BPDUs.

  **1.4** Other switches in the network will forward BPDUs but will not generate their own original BPDUs.

  **1.5** With all the calculation done, **the root bridge is elected** and all interfaces on the root bridge are designated ports which means that they are in forwarding state.

**2**. Each remaining switch will select **ONE** of its interface to be its **root port**. The interface with **the lowest root cost will be the root port** (root ports are also in a forwarding state).

Root cost is calculated based on the following:
```
10 Mbps => 100 STP cost
100 Mbps => 19 STP cost
1 Gbps => 4 STP cost
10 Gbps => 2 STP cost
```
![Switch logic of choosing root port]

The root port is selected based on 3 criteria:
- Lowest root cost.
- Lowest neighbor bridge ID.
- Lowest neighbor port ID. (STP Port ID = Priority + Port Number)

**IT IS CRUCIAL TO REMEMBER THAT THE TWO TIE-BREAKER IS IN THE NEIGHBOR NOT LOCAL**

**3** Each remaining collision domain will select ONE interface to be a designated port and the other port in the collision domain will be non-designated.
- The Switch with the lowest root cost will make its port designated
- If the root cost is the same, the switch with the lower bridge ID will make its port designated.
- The other switch will make its port non-designated (blocking).