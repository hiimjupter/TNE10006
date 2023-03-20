# TNE10006 - Lab 7a 
## Initial configuration
We will construct our network based on the following topology

![Network topology](https://github.com/Catcurity123/TNE10006/blob/main/Picture/Lab7/Network%20topology.png?raw=true)

The constructed network in Packet Tracer might look like this:

![Packet_tracer_topo](https://github.com/Catcurity123/TNE10006/blob/main/Picture/Lab7/Before_disable.png?raw=true)

## Part 1
**Network's components**
According to the picture above, we can acquire the following information about the switches:

* **Switch 3 (S3)** is the **Root Bridge** with the lowesst MAC address, there fore, **G0/1,2,5,6** are **Designated port**

* **Switch 4 (S4)** is the **Root Switch** with its port as follows:
  + **G0/5** is the root port with **lowest neighbour bridge ID**.
  + **G0/6** is the **alternative port** as it is connected to the Root Bridge and is not the root port.
  + **G0/3,4** will be Designated port with the lower cost.

* **Switch 1 (S1)** is the **Root Switch** with its ports as follows:
  + **F0/1** is the root port with the lower neighbour bridge ID (G0/1 is lower than G0/2).
  + **F0/2** is the **alternative port** as it is connected to the root bridge and is not the root port.
  + **F0/3,4** is the **alternative port** as its cost is higher than **G0/3,4**.

## Part 2
After disabling some interfaces according to the tutorial, we have the following topology:

![after_topology](https://github.com/Catcurity123/TNE10006/blob/main/Picture/Lab7/After_disable.png?raw=true)

We can then answer some questions in the Lab.

![answer1](https://github.com/Catcurity123/TNE10006/blob/main/Picture/Lab7/Answer.png?raw=true)

![answer2](https://github.com/Catcurity123/TNE10006/blob/main/Picture/Lab7/Answer2.png?raw=true)

## Part 3
We can change to alternative port by configuring some attribute of the Non-Root Switch, however, before doing that, let's calculate the cost of each interface according to the picture below.

![after_topology](https://github.com/Catcurity123/TNE10006/blob/main/Picture/Lab7/After_disable.png?raw=true)

**It is important to remember that the root cost is the total cost of the outgoing interfaces along the path to the root bridge, therefore:**
+ When a switch is directly connected to the root bridge, the root path cost for that switch is zero.
+ When a switch is not directly connected to the root bridge, the root path cost is calculated based on the cumulative cost of all the links between the switch and the root bridge. For example:



```
We only have 3 line of connection from Non-Root Bridge to the Root Bridge currently available:

+ F0/4 -> G0/4 -> G0/6 -> G0/6. (From S1 -> S4 -> S3)
+ G0/6 -> G0/6. (From S4 -> S3)
+ F0/2 -> G0/2. (From S1 -> S3)

The Cost for each line is as follows:
+ From S1 -> S4 -> S3 = 19 + 4 = 23 
+ From S4 -> S3 will be 4 as it is directly connected.
+ From S1 -> S3 will be 19 as it is directly connected.
```
Therefore, currently, the line from S1 -> S4 -> S3 is blocked as it has the largest cost. If we want to change to blocking intreface, we must increase the cost on other interface so that it will be larger than 23 or decrease the current cost so that it will be smaller than other line.

```
Suppose we want to change F0/4 to be the Root port for S1, we can increase the cost from F0/2 -> G0/2 to 24. 
=> Making S1 -> S4 -> S3 more efficient than from S1 -> S3
```

![change1](https://github.com/Catcurity123/TNE10006/blob/main/Picture/Lab7/Change1.png?raw=true)

```
Suppose we want to change F0/4 to be the Root port for S4, we can increase the cost from G0/6 -> G0/6 to 43. (Because From S4 -> S1 -> S3 currently is 23 + 19 = 42)
=> Making S4 -> S1 -> S3 more efficient than from S4 -> S3
```

![Change2](https://github.com/Catcurity123/TNE10006/blob/main/Picture/Lab7/Change2.png?raw=true)
