# NetPractice
This project is a general practical exercise that will let you discover networking.

You will have to configure small-scale networks. 

To do so, it will be necessary to understand how TCP/IP addressing works.

You will have to complete 10 levels of exercises.


## IP addresses: Networks and hosts

An IPv4 address is a 32-bit number (). It uniquely identifies a host (computer or other device, such as a printer or router) on a TCP/IP network.

IP addresses are normally expressed in **dotted-decimal** format, with four numbers separated by periods, such as 192.168.123.132.

Examine an IP address in binary notation to understand how *subnet masks* are used to distinguish between **hosts**, **networks**, and **subnetworks**, 

For example, the dotted-decimal IP address 192.168.123.132 is (in binary notation) the 32-bit number 11000000101010000111101110000100. This number may be hard to make sense of, so divide it into four parts of eight binary digits.

These 8-bit sections are known as **octets**. The example IP address, then, becomes 11000000.10101000.01111011.10000100. This number only makes a little more sense, so for most uses, convert the **binary address** into dotted-decimal format (192.168.123.132). The decimal numbers separated by periods are the octets converted from binary to decimal notation.

For a TCP/IP wide area network (WAN) to work efficiently as a collection of networks, the routers that pass packets of data between networks don't know the exact location of a host for which a packet of information is destined. Routers only know what network the host is a member of and use information stored in their route table to determine how to get the packet to the destination host's network. After the packet is delivered to the destination's network, the packet is delivered to the appropriate host.

For this process to work, an **IP address has two parts**. The first part of an IP address is used as a **network address**, and the last part as a **host address**. If you take the example 192.168.123.132 and divide it into these two parts, you get 192.168.123. Network .132 Host or 192.168.123.0 - network address. 0.0.0.132 - host address.


## Subnet mask
The second item, which is required for TCP/IP to work, is the **subnet mask**. The subnet mask is used by the TCP/IP protocol to determine whether a host is on the local subnet or on a remote network.

In TCP/IP, the parts of the IP address that are used as the network and host addresses **aren't fixed**. Unless you have more information, the network and host addresses above can't be determined. 
This information is supplied in another 32-bit number called a subnet mask. The subnet mask is 255.255.255.0 in this example. It isn't obvious what this number means unless you know 255 in **binary notation** equals 11111111. So, the subnet mask is 11111111.11111111.11111111.00000000.

Lining up the IP address and the subnet mask together, the network, and host portions of the address can be separated:

11000000.10101000.01111011.10000100 - IP address (192.168.123.132)
11111111.11111111.11111111.00000000 - Subnet mask (255.255.255.0)

The first 24 bits (the number of ones in the subnet mask) are identified as the **network address**. The last 8 bits (the number of remaining zeros in the subnet mask) are identified as the host address. It gives you the following addresses:

11000000.10101000.01111011.00000000 - Network address (192.168.123.0)
00000000.00000000.00000000.10000100 - Host address (000.000.000.132)

So now you know, for this example using a 255.255.255.0 subnet mask, that the network ID is 192.168.123.0, and the host address is 0.0.0.132. When a packet arrives on the 192.168.123.0 subnet (from the local subnet or a remote network), and it has a destination address of 192.168.123.132, your computer will receive it from the network and process it.

**Almost** all decimal subnet masks convert to binary numbers that are **all ones on the left and all zeros on the right**.

with the advent of classless inter-domain routing (CIDR), it's possible to use custom subnet masks that don't follow the strict classful pattern. These custom masks can have a **mix of ones and zeros** within the binary representation.





[Variable Length Subnet Table For IPv4](https://www.rfc-editor.org/rfc/pdfrfc/rfc1878.txt.pdf)



## Network classes
Internet addresses are allocated by the InterNIC, the organization that administers the Internet. These IP addresses are divided into classes. The most common of them are classes A, B, and C. Classes D and E exist, but aren't used by end users. Each of the address classes has a different default subnet mask. You can identify the class of an IP address by looking at its first octet. Following are the ranges of Class A, B, and C Internet addresses, each with an example address:

Class A networks use a default subnet mask of 255.0.0.0 and have 0-127 as their first octet. The address 10.52.36.11 is a class A address. Its first octet is 10 and falls between 1 and 126, inclusive.

Class B networks use a default subnet mask of 255.255.0.0 and have 128-191 as their first octet. The address 172.16.52.63 is a class B address. Its first octet is 172 and falls between 128 and 191, inclusive.

Class C networks use a default subnet mask of 255.255.255.0 and have 192-223 as their first octet. The address 192.168.123.132 is a class C address. Its first octet is 192 and falls between 192 and 223, inclusive.

In some scenarios, the default subnet mask values don't fit the organization's needs for one of the following reasons:


+ The physical topology of the network
+ The numbers of networks (or hosts) don't fit within the default subnet mask restrictions.

The next section explains how networks can be divided using subnet masks.

### Level 01
![image](https://github.com/user-attachments/assets/8405f5b4-dc4e-4f13-8b34-a851a2f95a4a)

Goal 1: Both computers have the same mask, I must put both of them in the same network so  I change MY PC's IP to 104.96.23.11

Goal 2: Same case. I change Host D's IP to 211.191.75.74

### Level 02
![image](https://github.com/user-attachments/assets/da8f2a17-5472-4714-98fa-9bd3678e7aa6)

#### Goal 1: 
+ 1st, change computer B's mask to 255.255.255.224.
+ 2nd, identify network.
  
  | Name|doted-decimal  |         binary address            |
  |-----|---------------|-----------------------------------|
  | mask|255.255.255.224|11111111.11111111.11111111.11100000|
  |   ip|192.168.041.222|11000000.10101000.00101001.11011110|
  |  and|192.168.041.192|11000000.10101000.00101001.11000000|
  |  net|192.168.041.192|11000000.10101000.00101001.11000000|
  |first|192.168.041.193|11000000.10101000.00101001.11000001|
  | last|192.168.041.222|11000000.10101000.00101001.11011110|
  | brdc|192.168.041.223|11000000.10101000.00101001.11011111|
  
+ 3rd, set Computer A's IP.
  Computer B has the network's last host number. I will assign the network's first host number 193.

  #### Goal 2: 
+ 1st, verify that C and D have the same mask

  | Name|doted-decimal  |         binary address            |
  |-----|---------------|-----------------------------------|
  |    C|255.255.255.252|11111111.11111111.11111111.11111100|
  |    D|            /30|11111111.11111111.11111111.11111100|

+ 2nd, choose a class C network. We can not use 127.0.0.0/8, as it is a **Loopback address**. A Loopback Address, also known as localhost, refers to an internal address that directs back to the local system. In IPv4, the loopback address is 127.0. 0.1. I chose 192.168.041.220
  
  | Name|doted-decimal  |         binary address            |
  |-----|---------------|-----------------------------------|
  | mask|255.255.255.252|11111111.11111111.11111111.11111100|
  |   ip|192.168.041.222|11000000.10101000.00101001.11011110|
  |  and|192.168.041.220|11000000.10101000.00101001.11011100|
  |  net|192.168.041.220|11000000.10101000.00101001.11011100|
  |first|192.168.041.221|11000000.10101000.00101001.11011101|
  | last|192.168.041.222|11000000.10101000.00101001.11011110|
  | brdc|192.168.041.223|11000000.10101000.00101001.11011111|
  
+ 3rd, set Computer C's IP and Computer D's IP.
  Set Computer C's IP to the network's first host number 221. I will assign the network's last host number 222.

### Level 03
  
![image](https://github.com/user-attachments/assets/81cf9e50-dea4-4dd1-be9b-a8049b373aa0)

We find the first switch. A switch is a device that connects multiple devices in a single network. 
The switch does not have interfaces since it only distributes packets to its local network, and cannot talk directly to a network outside of its own.

+ 1st, Detect the network we work with. 
  
  | Name|doted-decimal  |         binary address            |
  |-----|---------------|-----------------------------------|
  | mask|255.255.255.128|11111111.11111111.11111111.10000000|
  |   ip|104.198.089.125|01101000.11000110.01011001.01111101|
  |  and|104.198.089.000|01101000.11000110.01011001.00000000|
  |  net|104.198.089.000|01101000.11000110.01011001.00000000|
  |first|104.198.089.001|11000000.10101000.00101001.00000001|
  | last|104.198.089.126|11000000.10101000.00101001.01111110|
  | brdc|104.198.089.127|11000000.10101000.00101001.01111111|
  
+ 2nd, Set the same mask for hosts A, B, and C. 255.255.255.128
+ 3rd, set C's IP to the last host of the network 126. Set B's IP to the first host of the network.


  ### Level 04
  
![image](https://github.com/user-attachments/assets/b856284b-45fe-4bd8-9044-6330418bf009)
 
 We found a router. It is useless in this configuration cause we have only one network. 
 We do not need to connect different networks, that is what the router was designed for.

+ 1st, Detect the network we work with. 
  
  | Name|doted-decimal  |         binary address            |
  |-----|---------------|-----------------------------------|
  | mask|/23            |11111111.11111111.11111110.00000000|
  |   ip|085.126.119.132|01010101.01111110.01110111.10000100|
  |  and|085.126.118.000|01010101.01111110.01110110.00000000|
  |  net|085.126.118.000|01010101.01111110.01110110.00000000|
  |first|085.126.118.001|01010101.01111110.01110110.00000001|
  | last|085.126.118.254|01010101.01111110.01110110.11111110|
  | brdc|085.126.118.255|01010101.01111110.01110110.11111111|
  
+ 2nd, Set the same mask for hosts A, B, and C. /23
+ 3rd, set Router's R1's IP to the first host of the network 118.001. Set B's IP to the last host of the network 118.254.

  I believe this is a weird configuration ...
  
  |Interface|IP|
  |---------|-----|
  |R1|85.126.118.001/23|
  |A1|85.126.118.254/23|
  |BA|85.126.119.132/23|

  ...but the /23 has the last bit of the 3rd byte available, so x.x.118.x and x.x.119.x belong to the same network.


  ### Level 05

![image](https://github.com/user-attachments/assets/b42b183c-1c18-4a52-92b6-a0428d6fe393)

In this configuration the router is functional. There are two networks to connect. Since the router separates different networks, the range of possible IP addresses on one of its interfaces must not overlap with the range of its other interfaces. An **overlap** in the IP address range would imply that the interfaces are on the same network.

Here is the first time we see a route. A routing table is a data table stored in a **router** or a **network host** that lists the routes to particular network destinations. 

![image](https://github.com/user-attachments/assets/4e6635ed-dcb0-4fab-ba27-744f0cc0ad1d)


In NetPractice, the routing table consists of 2 elements:

+  (left) **Destination**: The destination specifies a **network address** on which a host is the end target of the packets. The route of default or 0.0.0.0/0, is the route that takes effect when no other route is available for an IP destination address. The default route will use the next-hop address to send the packets on their way without giving a specific destination. The default route will match any network.
+  (right) **Next hop** : The next hop refers to the **next closest router a packet can go through**. It is the IP address of the next router on the packet's way. Every single router maintains its routing table with a next-hop address.




+ This is our first router to connect two networks. Let's identify two networks, to fill route tables properly.
+ 1st, Identification of network A
  
  | Name|doted-decimal  |         binary address            |
  |-----|---------------|-----------------------------------|
  | mask|255.255.255.128|11111111.11111111.11111111.10000000|
  |   ip|086.184.183.126|01010110.10111000.10110111.01111110|
  |  and|086.184.183.000|01010110.10111000.10110111.00000000|
  |  net|086.184.183.000|01010110.10111000.10110111.00000000|
  |first|086.184.183.001|01010110.10111000.10110111.00000001|
  | last|086.184.183.126|01010110.10111000.10110111.01111110|
  | brdc|086.184.183.127|01010110.10111000.10110111.01111111|
  

+ 2nd, Identification of network B

  | Name|doted-decimal  |         binary address            |
  |-----|---------------|-----------------------------------|
  | mask|255.255.192.000|11111111.11111111.11000000.00000000|
  |   ip|161.154.207.254|10100001.10011010.11001111.11111110|
  |  and|161.154.192.000|10100001.10011010.11000000.00000000|
  |  net|161.154.192.000|10100001.10011010.11000000.00000000|
  |first|161.154.192.001|10100001.10011010.11000000.00000001|
  | last|161.154.255.254|10100001.10011010.11111111.11111110|
  | brdc|161.154.255.255|10100001.10011010.01110110.11111111|
  
+ 3rd, choose one IP for host A between  001 and  126 (86.184.183.124).
+ 4th, set Host A route table destination to other network (161.154.192.0/18) to and the next-hop to Interface R1 in router. I set it to another network cause there are only two networks.
+ 5th, Choose one IP for host B between 0001 and 254 (161.154.207.253).
+ 6th, set Host B route table destination to default to and next-hop to interface R2.
  
  ### Level 06
![image](https://github.com/user-attachments/assets/11d39f0b-d1f1-4310-95a5-08e25a769610)


We must connect Host A (61.240.134.227/24) to the internet. 
At this level, we deal with the internet through a hot IP. The internet connection cannot have an IP address in the reserved private IP ranges

|rfc 1918 name|       IP adress range       | Number of addresses|
|-------------|-----------------------------|--------------------|
|24-bit block |192.168.0.0 - 192.168.255.255| 65,536 |
|20-bit block |172.16.0.0 - 172.31.255.255  | 1,048,576|
|16-bit block |10.0.0.0 - 10.255.255.255    | 16,777,216|

we have a router with two interfaces.
The router's interface connecting to the internet is R2 (163.172.250.12). The interface connecting to the local network is R1 (163.172.250.1). I have to remark here that this IP for interface R1 is a "**loopback number**" the router uses internally inside the routes table. Loopback interfaces are virtual interfaces within the router itself. They are primarily used for internal routing and don't directly connect to any physical network. I remark on this point cause we have a different interface R1 IP (61.240.134.254) related to the network address range.
We got the hot IP from the internet in the routing table (61.240.134.0/31) with a next-hop thru router interface R2 (163.172.250.12)

  
+ 1st, identification of network A

  | Name|doted-decimal  |         binary address            |
  |-----|---------------|-----------------------------------|
  | mask|255.255.255.128|11111111.11111111.11111111.10000000|
  |   ip|061.240.134.227|00111101.11110000.10000110.11100011|
  |  and|061.240.134.128|00111101.11110000.10000110.10000000|
  |  net|061.240.134.128|00111101.11110000.10000110.10000000|
  |first|061.240.134.129|00111101.11110000.10000110.10000001|
  | last|061.240.134.254|00111101.11110000.10000110.11111110|
  | brdc|061.240.134.255|00111101.11110000.10000110.11111111|

  + 2nd, chose an IP for interface R1 (last-> 061.240.134.254),
  + 3rd, add it to host A's route table as next-hop for the default destination
  + 4th, set in router's route table default destination to internal interface R1
  + 5th, set in router's route table local network broadcast destination  (21.240.134.255/25) to internet interface R2.
  
### level 07

![image](https://github.com/user-attachments/assets/28fb3e6f-c761-4054-a747-5f5efef5f421)


In this case, we have two routers (R1 & R2) and three networks:
+ Network 1: Host A and interface 1 of Router 1 (Two IPs)
+ Network 2: interface 2 of router 1 and interface 1 of router 2 (Two IPs).
+ Network 3: Interface 2 of router 2 and Host C (Two IPs).

No overlap is allowed in the 3 network's IPs.

We require only two active iPs per network. So a  /30 mask fits our requirements: (net, first, last, broadcast)

For network 1, Interface 1 of router 1 has an IP 109.198.14.1. Together with the mask /30, we have:
|name     |     ip     | Interface |
|---------|------------|-----------|
|net      |109.198.14.0|           |
|first    |109.198.14.1| R11       |
|last     |109.198.14.2| A1        |
|broadcast|109.198.14.3|           |

For network 2, Interface 2 of router 1 has an IP 109.198.14.254. Together with the mask /30, we have:
|name     |     ip       | Interface |
|---------|--------------|-----------|
|net      |109.198.14.252|           |
|first    |109.198.14.253| R21       |      
|last     |109.198.14.254| R12       |
|broadcast|109.198.14.255|           | 

For network 3, the only restriction is not to overlap with previous networks.
|name     |     ip      | Interface |
|---------|-------------|-----------|
|net      |109.198.14.40|           |
|first    |109.198.14.41| R22       |      
|last     |109.198.14.42| C1        |
|broadcast|109.198.14.43|           | 

Now the four routing tables are filled like this

|Table   |destination|next-hop|
|--------|----------------|-------------|
|Host A  |109.198.14.40/30|109.198.14.1|
|Host C  |109.198.14.0/30 |109.198.14.41|
|Router 1|109.198.14.40/30|109.198.14.253|
|Router 2|109.198.14.0/30|109.198.14.254|

### Level 8

![image](https://github.com/user-attachments/assets/b2964f72-c9cc-4afe-8614-f4fa85225a2a)

We see that internet addresses are in the range 152.236.170.0/26.

Internally we require 3 subnets in this range.  a netmask /27 is not enough for 3. We will use /28.
We have a hint inside the route table of router 2. The next hop is the IP 152.236.170.62

  | Name|doted-decimal  |         binary address            |
  |-----|---------------|-----------------------------------|
  | mask/26|255.255.255.240|11111111.11111111.11111111.11000000|
  |   ip   |156.236.170.001|00111101.11110000.10000110.00000001|
  |  and   |156.236.170.000|00111101.11110000.10000110.00000000|
  | net0/26|156.236.170.000|00111101.11110000.10000110.00000000|
  | ip net1|156.236.170.062|00111101.11110000.10000110.00111110|
  | mask/28|156.236.170.062|11111111.11111111.11111111.11110000|
  | net1   |156.236.170.048|00111101.11110000.10000110.00110000|
  | net2/28|156.236.170.032|00111101.11110000.10000110.00100000|
  | net3/28|156.236.170.016|00111101.11110000.10000110.00010000|
  | net4/28|156.236.170.000|00111101.11110000.10000110.00000000|

  Once I selected the 3 networks, as each network has only two devices I will use the first and the last active IP from each network.
  
| Network |Interface| IP            |
|---------|---------|---------------|
|Network 1| R21     |156.236.170.049|
|Network 1| R13     |156.236.170.062|
|Network 2| D1      |156.236.170.033|
|Network 2| R23     |156.236.170.046|
|Network 3| R22     |156.236.170.017|
|Network 3| C1      |156.236.170.030|
  
  
## level 9

![image](https://github.com/user-attachments/assets/d9130b17-79f1-4b7f-b1f5-0e42d1bbb0a7)

We have 5 networks:

|Network|Hosts               | restrictions|
|-------|--------------------|-------------------------------------------------|
|1      | Host A & Host B    | netmask = 255.255.255.128(/25)                  |
|2      | Router 1 & Router 2| ip= 163.172.250.1 netmask = 255.255.255.252(/30)|
|3      | Host c             | none                                            |
|4      | Host d             | IP =82.95.53.200 netmask =255.255.192.0 (/18)   |
|5      | internet           |                                                 |

+ 1st, calculate network 4.
+ 

  | Name   |doted-decimal  |         binary address            |
  |--------|---------------|-----------------------------------|
  | mask/18|255.255.192.000|11111111.11111111.11000000.00000000|
  |   ip   |082.095.053.200|01010010.01011111.00110101.11001000|
  |  and   |082.095.000.000|01010010.01011111.00000000.00000000|
  | net4/18|082.095.000.000|01010010.01011111.00000000.00000000|

The network is 82.95.0.0/18. I choose the second IP for this network as 82.95.0.1

+ 2st, Calculate network 2.
  

  | Name   |doted-decimal  |         binary address            |
  |--------|---------------|-----------------------------------|
  | mask/30|255.255.255.252|11111111.11111111.11111111.11111100|
  |   ip   |163.172.250.001|10100011.10101010.11111010.00000001|
  |  and   |163.172.250.000|10100011.10101010.11111010.00000000|
  | net2/30|163.172.250.000|01010010.10101010.00000000.00000000|

The network is 163.172.250.000. it has only two active machines 163.172.250.1 (used) and 163.172.250.2 (available)

+ 3st, calculate network 3.
+ 
I will select another /18 compatible with network 4.

 Let's choose 82.95.0.16/18 with active IP (82.95.0.17 and 82.95.0.18)


+ 4th, Calculate network 1
  
Must use a /25 mask, but compatible with already selected networks. I start with the IP used for network 4

  | Name   |doted-decimal  |         binary address            |
  |--------|---------------|-----------------------------------|
  | mask/25|255.255.255.252|11111111.11111111.11111111.10000000|
  |   ip   |082.095.053.200|01010010.01011111.00110101.11001000|
  |  and   |082.095.053.128|01010010.01011111.00110101.10000000|
  | net1/25|082.095.053.128|01010010.01011111.00110101.10000000|


The three active IP I selected for this network are 82.95.53.129, 82.95.53.130, and 82.95.53.131


+ 5th, I define a internet network with a mask enough for all networks /25 /18. i work with /23
  
  | Name   |doted-decimal  |         binary address            |
  |--------|---------------|-----------------------------------|
  | mask/25|255.255.255.252|11111111.11111111.11111110.00000000|
  |   ip   |082.095.053.200|01010010.01011111.00110101.11001000|
  |  and   |082.095.052.000|01010010.01011111.00110100.00000000|
  | net1/25|082.095.052.000|01010010.01011111.00110100.00000000|


  

+ 1st identify internet network

  | Name|doted-decimal  |         binary address            |
  |-----|---------------|-----------------------------------|
  | mask|255.255.255.254|11111111.11111111.11111111.11111110|
  |   ip|061.240.134.227|00111101.11110000.10000110.00000001|
  |  and|061.240.134.000|00111101.11110000.10000110.00000000|
  |  net|061.240.134.000|00111101.11110000.10000110.00000000|
  |first|078.147.070.129|01001110.10010011.01000110.10000001|
  | last|078.147.070.129|01001110.10010011.01000110.10000001|
  | brdc|078.147.070.129|01001110.10010011.01000110.11111111|
