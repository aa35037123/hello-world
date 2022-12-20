# 計網概HW2
p6. 
The shortcoming of manually configure a host's IP address are:
1. The scaling problem could happen. When hosts of network increases, the speed of DHCP server giving a IP address to host will be very slow.
2. The secure problem could happen. Manually configuring IP address can not  detect whether host is authorized. If unauthorized hosts ask DHCP server for IP, that will cause wasting of IP address.
p7
a. No. When fabric use shared bus, there is only one packet can go through switch fabrics at the same time.
b. Yes. When fabric use crossbar, two packets are forwarded at the same time is possible as long as they are forwarded to different output ports.
c. No. When fabric use shared bus, if two packets are forwarded to the same output port, one of them have to wait until other one finish transmission.
p10. 
a.

| Prefix Match | Link Interface |
| ------------ | -------------- |
|11100000 00000000 |        0        |
|11100000 00000001|      1          |
|1110000 0 |              2  |
|1110000 0|             2   |
|11100001 1|          2      |
| otherwise| 3         |


b. Use longeset prefix matching to find the appropriate link interface
1. First datagram doesn't match any entries above, it should go to link interface 3
2. Second datagram match the first entry, it should go to link interface 0
3. Third datagram match the forth entry, it should go to link interface 2
p16:
- 192.168.56.128/26 tells that first 26 bits in subnet is fixed, so the last 8 bits must be 10xxxxxx. 
	Example: 192.168.56.129 is one IP address of this subnet.
- 192.168.26.32/27tells that first 27 bits in subnet is fixed, so the last 8 bits must be 001xxxxx. So the vaild IP address range is: 192.168.26.32 to 192.168.26.63, total 32 IP address.
	32 / 4 = 8 => each subnet can be distributed for 8 IP address
	- subnet1:192.168.26.32 to 192.168.26.39, prefix is 192.168.26.32/29
	- subnet2:192.168.26.40 to 192.168.26.47, prefix is 192.168.26.40/29
	- subnet3:192.168.26.48 to 192.168.26.55, prefix is 192.168.26.48/29
	- subnet4:192.168.26.56 to 192.168.26.63, prefix is 192.168.26.56/29
p19:
*MTU: link可以接受的最大packet大小，隨著link不同而變動，單位是byte*
- Because IP datagram header is 20 bytes, so actual data is 1600 - 20 = 1580.
- The actual data in MTU is 500-20 = 480
- 1580 / 480 = 3.3
- Datagram can be divided into 4 fragments:
	1. length = 500, actual data size= 480, ID = 291, fragflag = 1, offset = 0
	2. length = 500, actual data size = 480, ID = 291, fragflag = 1, offset = 480 / 8 = 60
	3. length = 500, actual data size = 480, ID = 291, fragflag = 1, offset = 480 x 2 / 8 = 120
	4. length = 160, actual data size = 140, ID = 291, fragflag = 0, offset = 480 x 3 / 8 = 180
p28:
- i: in the ith loop
- Each row in the table represent minimum cost path currently from node z to each node after the ith run with distance vector algorithm
- Because we only want to know minimum cost path to each node start at z, so I only do table about z

| i | z    |   u  |   v  |x | y |
| -------- | --- | --- | --- | -------- | -------- |
|    0      |   0  |  ∞   |  6   |   2       |     ∞     |
|     1     |  0   |  7   | 5    |   2       |     5     |
|     2     | 0    |  6   |  5   |    2      |    5      |
| 3    |   0  |  6   | 5    | 2     | 5     |

- distance table start at node z:
	- value means that minimum cost path from z to that node


| z    |   u  | v | x | y |
| --- | --- | -------- | -------- | -------- |
|   0  |   6  | 5     | 2    | 5     |


p29:
- Suppose that there are "n" nodes in graph, the maximum number of iterations required before the distributed algorithm converges is "n-1"
- All the adjacent nodes to current node will know the minimum cost path from current node after 1st iteration.
	Consider that the structure of graph is like linked list. The longest path in this graphstart at s, end at u, it takes "n-1" edges. If we want to know minimum cost path from s to u with distance vector algorithm, we need "n-1" iteration to send information about s to u, since only adjacent nodes to current can receieve current node's information.
- If there are more than "n-1" iteration, the graph must have negative  cycle.

p41:
- Congestion control: 
	- It control the traffic entering the network.
	- It prevent packet drops in transmission
- Flow control:
	- It controls the traffic from a particular sender to a receiver.
	- It prevents the receiver from being overwhelmed by the sender.
- "Recrive window size" in sender side provide flow control with TCP

p44:
a. 
- Cwnd increases from 6 to 12 MSS, it takes total 6 RTTs
b. 
- 6 MSS was sent in the first RTT
- 7 MSS was sent in the secont RTT
- 8 MSS was sent in the third RTT
- 9 MSS was sent in the forth RTT
- 10 MSS was sent in the fifth RTT
- 11 MSS was sent in the sixth RTT
=> By 6 RTTs, there are total(6+7+8+9+10+11) = 51 MSS are sent, so the average throughout is 51 / 6 =  8.5(MSS / RTT)

R18:
- The 5 PCs use DHCP protocol to access IP address.
- Generally, the wireless router includes a DHCP server. Below are steps that how client connect to DHCP server:
	1. client send DHCP request message to DHCP server ask for IP address
	2. DHCP server will send offer message and available IP address to client
	3. client send DHCP request message to DHCP server, which tell that client can use this IP address
	4. DHCP server will send ACK to client, which tell that client can use this IP address
- Since ISP only assigned one IP address to the wireless router, the wireless router will use NAT to distribute IP address to every PCs, help PCs connect to network.