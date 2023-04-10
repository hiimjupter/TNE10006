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

## 5. IPv4 

### 5.1 IPv4 header

![IPv4](https://github.com/Catcurity123/TNE10006/blob/main/Final%20Written%20Exam/Picture/IPv4_Packet-en.svg.png)

**1. Version - 4bits**: Identify the version of IP used. IPv4 = 4 (0100), IPv6 = 6 (0110)

**2. Internet Header Length (IHL) - 4 bits**: This field is used to indicate the total length of the header.

This will identify the length of the header in **4-byte increments**, meaning that if the value of this field is 5 then the length of IPv4 is 20 bytes.

The minimum value of IPv4 header is 20 bytes (5 in IHL) and the maximum value is 60 bytes (15 in IHL).

**3. Differentiated Services Code Point (DSCP) field - 6 bits**: used for QoS (quality of service) and prioritize delay-sensitive data (streaming, video).

**4. Explicit Congestion Notification (ECN) field - 2 bits**: provides end-to-end notification of network congestion without dropping packets. This is optional and will require both endpoints.

**5. Total Length Field - 16 bits**: Indicate the total length of the packet(L3 header + L4 segment). Measured in bytes. Minimum value of 20.
 
**6. Identification field - 16 bits**: If a packet is fragmented due to being too large, this field is used to identify which packet the fragment belongs to. 

Fragments of the same packet will have their own IPv4 header with the same value in this field.

Packets are fragmented if larger than the MTU (1500). 

**7. Flag field - 3 bits**: used to control/identify fragments. 

Bit 0: Reserved, always set to 0

Bit 1: Don't Fragment (DF bit), used to indicate a packet that should not be fragmented.

Bit 2: More Fragments (MF bit), set to 1 if there are more fragments in the packet. Unfragmented packets will always have their MF bit set to 0.

**8. Fragment Offset field - 13 bits**: used to indicate the position of the fragment with in the original Unfragmented IP packet.

Allow fragmented packets to be reassembled even if the fragments arrive out of order.

**9. Time to live field - 8 bits**: A router will drop a packet with a TTL of 0, used to prevent infinite loops.

**10. Protocol field - 8 bits**: indicates the protocol of the encapsulated L4PDU, 6 is TCP, 17 is UDP, 1 is ICMP, 89 is OSPF.

**11. Header Checksum field - 16 bits**: A calculated checksum used to check for errors in the IPv4 header.

When a router receives a packet, it calculates the checksum of the header and compares it to the one in this field of header.

If they do not match the router will drop the packet.

**12. Source/Destination IP address 32 bits each**: used to indicate the address of the sender and receiver.

**Type of IPv4 Address**:

**Private Network**: 
- 10.0.0.0 – 10.255.255.255 (10.0.0.0/8)
- 172.16.0.0 – 172.31.255.255 (172.16.0.0/12)
- 192.168.0.0 – 192.168.255.255 (192.168.0.0/16)

**Loopback**: 127.0.0.1 

**Link-Local address**: 169.254.0.0 - 169.254.255.255

**Test-net address**: 192.0.2.0 - 192.0.2.255.

## 6. IPv6
Typically, an enterprise request an IPv6 address from ISP will receive a /48 block.

Typically, IPv6 subnets use a /64 prefix length.

That means an enterprise has 16 bits to use to make subnets.

The remaining 64 bits can be used for hosts

![IPv6](https://github.com/Catcurity123/TNE10006/blob/main/Final%20Written%20Exam/Picture/IPv6.png)

Here is an example of how to find the prefix.

![Exampe](https://github.com/Catcurity123/TNE10006/blob/main/Final%20Written%20Exam/Picture/Example.png)

Some more examples for further practice.

![example2](https://github.com/Catcurity123/TNE10006/blob/main/Final%20Written%20Exam/Picture/practice%202.png)

## 7. TCP Connection Management
Transmission Control Protocol - TCP is defined in RFC 793, containing the following characteristics:

+ **Connection-oriented**: Coonection must be established data transmission can be deployed.

+ **Guaranteed Delivery**: ACK will be sent if received data, or else the data will be retransmitted.

+ **Assure in-order Delivery**: Sequence number is used to reassemble the segments.

+ **Flow control implementation**: Window size is used to ensure appropriate connection rate between sender and receiver.


**TCP Segment**

![TCP Segment](https://github.com/Catcurity123/TNE10006/blob/main/Final%20Written%20Exam/Picture/TCP%20Segment.png)

**1. Source port - 16 bits**: Specifies the port number on the sending device that is used for the communication. Typically selected randomly from 1024 - 65535.

**2. Destination port - 16 bits**: Specifies the port number on the receiving device that is used for the communication.

**3. Sequence number - 32 bits**: Specifies the sequence number of the first byte of data in the segment. 

**4. Acknowledgment number - 32 bits**: Specifies the acknowledgment number of the next expected byte of data. This is used to acknowledge the receipt of data.

**5. Data offset - 4 bits**: Specifies the size of TCP header in 32-bit words.

**6. Reserved - 6 bits**: Unused bits that are reserved for future use.

**7. Control bits - 6 bits**: A set of bits that control various aspects of the TCP connection.
+ URG (Urgent pointer field)
+ ACK (AAcknowledgment number field)
+ PSH (push function)
+ RST (reset the connection)
+ SYN (synchronize sequence numbers)
+ FIN (no more data)

**8. Window size - 8 bits**: Specifies the number of bytes that the receiving device is willing to accept.

**9. Check sum - 8 bits**: A value that is calculated based on the contents of TCP used to detect errors.

**10. Urgent pointer - 8 bits**: Indicates whether the segment contains urgent data.

**11. Options**: additional field.


**TCP's 3-way handshake**

TCP's 3-way handshake is a mechanic that TCP use to initiate the conncetion in layer 4.

![3-way hand](https://github.com/Catcurity123/TNE10006/blob/main/Final%20Written%20Exam/Picture/TCP.png	)

**Sequence number** is based on number of bytes transmitted not segment, initial sequence number exchange in SYN and SYN-ACK packets.

**Acknowledgement number** acknowledge next bytes expecting, do not acknowledge last byte received.


![3-way hand1](https://github.com/Catcurity123/TNE10006/blob/main/Final%20Written%20Exam/Picture/3way.png)

![3-way hand2](https://github.com/Catcurity123/TNE10006/blob/main/Final%20Written%20Exam/Picture/3way2.png)

It is **important** to remember that sequence number and acknowledge number are measurement of bytes being sent not segment. and the ACK in data transmission is different from ACK in 3 way handshake

![import]()https://github.com/Catcurity123/TNE10006/blob/main/Final%20Written%20Exam/Picture/import.png

**Another key point of TCP is that it is full-duplex** meaning that both parties can send and receive data at the same time.

![full-duplex](https://github.com/Catcurity123/TNE10006/blob/main/Final%20Written%20Exam/Picture/full-duplex.png)

**4-way closure to close the connection**

![4-way closure](https://github.com/Catcurity123/TNE10006/blob/main/Final%20Written%20Exam/Picture/4wayclosure.png)
