# TNE10006 Cheat Sheet

## 1. Reference Model and Data Encapsulation

**The OSI Reference Model**

![OSI](https://github.com/Catcurity123/TNE10006/blob/main/Final%20Written%20Exam/Picture/OSIModel.png)


**The TCP/IP Protocol Model**

![TCP/IP](https://github.com/Catcurity123/TNE10006/blob/main/Final%20Written%20Exam/Picture/TCP_IP%20Model.png)


**TCP/IP and OSI comparison**

![compare](https://github.com/Catcurity123/TNE10006/blob/main/Final%20Written%20Exam/Picture/TCPIP%20and%20OSI%20comparison.png)


**Protocol Data Units**

![PDU](https://github.com/Catcurity123/TNE10006/blob/main/Final%20Written%20Exam/Picture/PDU.png)

+ Data - The general term for the PDU used at the application layer.

+ Segment - Transport layer PDU.

+ Packet - Network layer PDU.

+ Frame - Data Link layer PDU.

+ Bits - Physical layer PDU used when physically transmitting data over the medium.

## 2. Physical layer

**Bandwidth Terminology**

+ **Bandwidth**: is the capacity at which a medium can carry data.

+ **Latency**: refers to the amount of time, including delays, for data to travel from one given point to another.

+ **Throughput**: is the measure of the transfer of bits accross the media over a given peroid of time.

+ **Goodput**: is the measure of usable data transferred over a given period of time.

## 3. Data Link layer

The Data Link Layer prepares network data for the physical network. It is responsible for network interface card to network interface card communications.

IEEE 802 LAN/MAN layer consists of two sublayers:
+ **Logical Link Control(LLC)**: This sublayer allows for communication between Data Link to upper layer.

+ **Media Access Control(MAC)**: THis sublayer is responsible for data Encapsulation and media access control to lower layer.

There are two types of topologies used when describing LAN and WAN:

+ **Physical topology**: Identifies the physical connections and how end devices and intermediary devices are connected.

+ **Logical topology**: Refers to the way a network transfers from one node to the next.

### 3.1 WAN topologies

+ **Point-to-Point**: consists of a permanent link between two endpoints.

+ **Hub and Spoke**: refers to the network where endpoints can only reach each other by going through the central site.

+ **Mesh**: Provide high availability but requires every end system to interconnect to every other system.

### 3.2 LAN topologies
In multiaccess LANs, end deviecs are interconnected using star or extended sta topologies, in which end devices are connected to a central intermediary device.

**Legacy LAN topologies**
Early Ethernet and legacy Token Ring LAN technologies include:

+ **Bus**: where all end systems are chained to each other and terminated in some form on each end.

++ **Ring**: End systems are connected to their respective neighbor forming a ring.

### 3.3 Half and Full Duplex communication

**Half-duplex communication** allows only one device to send or receive at a time on a shared medium.

**Full-duplex communication** allows devices to transmit and receive data simultaneously on the shared media.

### 3.4 Access Control Methods

There are two basic access control methods for shared media:

**Contention-based access** : Where all nodes are operating in half-duplex, competing for the use of the medium. However, only one device can send at a time. Therefore, methods are required to handle this:

* **Carrier sense multiple access with collision detection (CSMA/CD)** used on legacy bus-topology Ethernet LANs

* **Carrier sense mutiple access with collision avoidance (CSMA/CA)** on wireless LANs

**Controlled access**: each node has to wait for their turn to access the network medium

**CSMA/CD**:

If two devices transmit at the same time, a collision will occur. For legacy Ethernet LANs, both devices will detect the collision on the network. This is the collision detection(CD) portion of CSMA/CD.

 The NIC compares data transmitted with data received, or by recognizing that the signal amplitude is higher than normal on the media. The data sent by both devices will be corrupted and will need to be resent.

 **CSMA/CA**

CMSA/CA uses a method similar to CSMA/CD to detect if the media is clear. CMSA/CA uses additional techniques. In wireless environments it may not be possible for a device to detect a collision. CMSA/CA does not detect collisions but attempts to avoid them by waiting before transmitting.

device that transmits includes the time duration that it needs for the transmission. All other wireless devices receive this information and know how long the medium will be unavailable.

### 3.5 Fram Fields
Framing breaks the stream into decipherable groupings, with control information inserted in the header and trailer as values in different fields.

![Frame Fields](https://github.com/Catcurity123/TNE10006/blob/main/Final%20Written%20Exam/Picture/DataFrame.png)

**1. Frame start and stop indicator flags**: used to identify the beginning and end limites of the frame.

**2. Addressing**: indicates the source and destination nodes on the media.

**3. Type**: Identifies the Layer 3 protocol in the data field.

**4. Control**: Identifies special flow control services such as quality of service(QoS) or voice over ip(VoIP)

**5. Data**: Contains the frame payload.

**6. Error Detection**: included after the data to form the trailer.


## 4. Ethernet Frames 

According to Maximum Transmission Unit (MTU), the minimum Ethernet frame size is 64 bytes and maximum is 1518 bytes(1500 data and 18 Ethernet bits)

![Ethernet Frame](https://github.com/Catcurity123/TNE10006/blob/main/Final%20Written%20Exam/Picture/Ethernet%20Frame.png)

**1. Preamble and Start Frame Delimiter Fields** are used to synchronize between sending and receiving devices. Preamble is 7 bytes SFD is 1 byte.

**2. Destination MAC address field**: 6 bytes of the identifier for the inteded recipent.

**3. Source MAC address field**: 6 byte identifier of the originating NIC.

**4. Type/Length** Identifier for upper layer protocol. IPv4 is 0x800, IPv6 is 0x86DD, ARP is 0x806. 2 bytes.

**Frame Check Sequence Field**: FCS consists of 4 bytes that is used to detect error in a frame. It uses a cyclic redundancy check (CRC) to check for changes in the data.
