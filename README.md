# NetPractice
This project is a general practical exercise to let you discover networking.

You will have to configure small-scale networks. 

To do so, it will be necessary to understand how TCP/IP addressing works.

You will have to complete 10 levels of exercises.


## IP addresses: Networks and hosts

An IPv4 address is a 32-bit number (). It uniquely identifies a host (computer or other device, such as a printer or router) on a TCP/IP network.

IP addresses are normally expressed in **dotted-decimal** format, with four numbers separated by periods, such as 192.168.123.132.

To understand how *subnet masks* are used to distinguish between **hosts**, **networks**, and **subnetworks**, examine an IP address in binary notation.

For example, the dotted-decimal IP address 192.168.123.132 is (in binary notation) the 32-bit number 11000000101010000111101110000100. This number may be hard to make sense of, so divide it into four parts of eight binary digits.

These 8-bit sections are known as **octets**. The example IP address, then, becomes 11000000.10101000.01111011.10000100. This number only makes a little more sense, so for most uses, convert the **binary address** into dotted-decimal format (192.168.123.132). The decimal numbers separated by periods are the octets converted from binary to decimal notation.

For a TCP/IP wide area network (WAN) to work efficiently as a collection of networks, the routers that pass packets of data between networks don't know the exact location of a host for which a packet of information is destined. Routers only know what network the host is a member of and use information stored in their route table to determine how to get the packet to the destination host's network. After the packet is delivered to the destination's network, the packet is delivered to the appropriate host.

For this process to work, an **IP address has two parts**. The first part of an IP address is used as a **network address**, the last part as a **host address**. If you take the example 192.168.123.132 and divide it into these two parts, you get 192.168.123. Network .132 Host or 192.168.123.0 - network address. 0.0.0.132 - host address.


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

Class A networks use a default subnet mask of 255.0.0.0 and have 0-127 as their first octet. The address 10.52.36.11 is a class A address. Its first octet is 10, which is between 1 and 126, inclusive.

Class B networks use a default subnet mask of 255.255.0.0 and have 128-191 as their first octet. The address 172.16.52.63 is a class B address. Its first octet is 172, which is between 128 and 191, inclusive.

Class C networks use a default subnet mask of 255.255.255.0 and have 192-223 as their first octet. The address 192.168.123.132 is a class C address. Its first octet is 192, which is between 192 and 223, inclusive.

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

Goal 1: 
+ 1st, change computer B's mask to 255.255.255.224.
+ 2nd, identify network.
  
  | Name|doted-decimal  |         binari address            |
  |-----|---------------|-----------------------------------|
  | mask|255.255.255.224|11111111.11111111.11111111.11100000|
  |   ip|192.168.041.222|11000000.10101000.00101001.11011110|
  |  and|192.168.041.192|11000000.10101000.00101001.11000000|
  |  net|192.168.041.192|11000000.10101000.00101001.11000000|
  |first|192.168.041.193|11000000.10101000.00101001.11000001|
  | last|192.168.041.222|11000000.10101000.00101001.11011110|
  | brdc|192.168.041.223|11000000.10101000.00101001.11011111|
  
+ 3rd, set Computer A's IP.
  Computer B has the network's first host number. I will assign the network's last host number 222. 
