## Network

What is network?

network: connect devices / devices share information

### 1. Introduction

What are the two ways computers can connect to the network?

wireless --- WIFI (device: Access Point)

cable --- Ethernet (device: switch)

How many protocols are used when one computer accesses another computer?

Ethernet / TCP: sending and receiving data

HTTP: accessing the web

SMTP: email



nodes: 

1. switch, router(control traffic flow)

2. endpoint, host(send and receive the bulk of traffic)

LAN: Local Area Network, a network in a local area

WAN: Wide Area Network, connect networks that are separated. Can call enterprise network.

### 2. Cabling Devices

Ethernet has physical layer, Media Access Control layer(保证各个不同速率cable的通信). Ethernet protocol describes physical links, and how data is formatted.

| LAN  | Ethernet | WIFI   |
| ---- | -------- | ------ |
| 802  | 802.3    | 802.11 |

Host has a MAC(Media Access Control) address and IP(Internet protocal) address

| MAC                                | IP                                       |
| ---------------------------------- | ---------------------------------------- |
| unique, used within a LAN segment. | access hosts on a different LAN segment. |

How many MAC address does a computer have?

Computer can have have multiple MAC Addresses**, **one  for each Network interface

### 3. OSI Model

| Capital | Layer        | Function                                               |
| ------- | ------------ | ------------------------------------------------------ |
| Please  | Physical     | manage physical components, encode data                |
| Do      | Data Link    | create logical link between devices, add local address |
| Not     | Network      | add network address, add routing                       |
| Throw   | Transport    | transport data between endpoints                       |
| Sausage | Session      | create session between applications                    |
| Pizza   | Presentation | data conversion and format                             |
| Away    | Application  | access network                                         |

### 4. IP Address

| IP   | IP Bit    | Belongs to |
| ---- | --------- | ---------- |
| 192  | 1100 0000 | Network    |
| 168  | 1010 1000 | Network    |
| 0    | 0000 0000 | Host       |
| 100  | 0110 0100 | Host       |

IP address are two address in on: Host Address + Network Address

| Class | Octets                                                       | Range                     |
| ----- | ------------------------------------------------------------ | ------------------------- |
| A     | Device, 1 Octet - 1 bit = 7 bits<br /> 128 Networks, 16M Hosts | 1.0.0.0-126.0.0.0         |
| B     | Device, 2 Octets - 2 bits= 14 bits <br />16T Networks, 65T Hosts | 128.0.0.0-191.255.0.0     |
| C     | Device, 3 Octets - 3 bits=21bits <br />2M Networks, 255 Hosts | 192.0.0.0-223.255.255.0   |
| D     | Multicast                                                    | 224.0.0.0-239.255.255.255 |
| E     | Reserved                                                     |                           |

Cidr / Subnet mask: break large network into small ones

1 for network, 0 for host

172.16.1.0/24   24 means first 24 bits are used for network

### 5. IP Address In Depth

VLSM: Variable Length Subnet Mask, create subnets on different size

Uni-Cast Traffic: device only send traffic to on other device

Multi-Cast Traffic:

Broadcast Traffic: router never forward broadcast message

broadcast address: each host bits are set to 1 (172.16.2.255/24)

network address: every host bits are set to 0 (172.16.2.0/24)

RFC 1918 Private Address

10.0.0.0/8

172.16.0.0/12

192.168.0.0/16

NAT Network address Translation

### 6. TCP/IP

Application

Transport: Use TCP/UDP protocal, create and maintain  conversations between applications processors on hosts. Use port number to track session.

Network: use IP, make sure data from one host can find a way to another host. IP header contains source and destination

Data link, responsible for delivery of traffic on a single Network segment or LAN.

Physical: move data from device to device



The combination of IP and port number enable system to have more than one session open at a time and track them.



A model is a set of layers that describe how network hardware and software works together. The goal of OSI model is to allow different protocols and vendors to work together. 

In application layer we talk about protocols like HTTP for web browsing. These application creates process which listen on particular ports. That's the job of transport layer which uses tcp/udp protocols. The network layer use IP protocol, the physical and data link layer move the data from device to device that is across switches, access points routers and other network equipment.





### 7. How TCP and UDP work

Two protocols in the transport layer. These are TCP and UDP. We are going to see how they get information form one application to another and their different approaches to their job.

Two devices on a network rely on IP to deliver information between each other. This happens on layer 3 (Network) which may include routing packets across several networks. At layer 4 (Transport) though we see very different behavior. The transport layer doesn't care too much about the networks in between, it doesn't care too much about the devices themselves, instead, it cares more about **getting data between applications**.

TCP and UDP share things in common. For example they both have headers and they both have port numbers. But as you can see in the headers,  there's a lot more going on with TCP than UDP. That's because TCP supports a lot of features while UDP is extremely lightweight.

In the header, you will see source and destination ports. The port are used to **identify** the applications on each device. In this way ports are like addresses for applications. This is similar to how the devices themselves have IP addresses. When an application starts a conversation it chooses a protocol to use as well as a random source port value from 1024-65535. This port number is not already in use on the device, one port number can not be given to more than one process at a time. The destination port number is the port number of the server application. It's usually a well-known value(0-1023). If we were using HTTP for web browsing, the port will normally be port 80. 

By making a port well-known, it's easy for client to guess that port the destination application will use. Of course a server application could be configured to use a non-standard. Use different port give us really useful feature called **multiplexing**. *It is a way that one host to have several applications accessing the network at one.* They all share the one network card the one network stack the one IP address but they each use different ports. 

A network application uses a concept called **socket**, it made up of a local IP address, a local port number and a protocol. As port numbers are unique so are sockets. Therefore, a socket can identify which application the network data belongs to. 

| Local IP   | Local Port | Protocol |
| ---------- | ---------- | -------- |
| 172.16.0.1 | 80         | TCP      |

One single application can also access to network many time a once, but as it is only one application have one port and one ip. So how can you tell from one to the other? It needs to look at the combination of the local socket information and the remote socket information. It can find all of these in layer 3 and layer 4 headers. It now has five pieces of information. This called **5-tuple**

| Local IP   | Remote IP | Local Port | Remote Port | Protocol |
| ---------- | --------- | ---------- | ----------- | -------- |
| 172.16.0.1 | 10.0.0.1  | 80         | 34761       | TCP      |

TCP has additional features while UDP is lightweight. For example, TCP has connection-oriented(TCP will build and track a connection between applications on a pair of hosts before sending data, when they are done, TCP will close their connection) while 

UDP is connectionsless. UDP doesn't start a connection, it just starts sending data without worrying any of those details.

TCP and UDP also have very different feelings about what to do about **errors**. UDP does care about errors, if a packet or segment goes missing, UDP doesn't worry, it just move on to the next piece of data. TCP does care about lost data. The receiver must acknowledge all the data that has received and if data is lost TCP will manage the retransmission. Because of this TCP is known as **reliable** while UDP is known as **unreliable**.

It also leads into a TCP feature called **windowing**. It is where both sides of conversation agree on how much data can be send at once before the receiver to acknowledge. It's value is called window size. If there is no data loss, the window size can dynamically grow if there is data loss, the window size will dynamically shrink. 

TCP used sequence numbers in the header to track the order that segments should be processed. This maybe critical for some applications, but it does add extra overhead in processing time. This is not important for other applications which maybe why they use UDP. UDP does not care about the order of the data is in. You maybe wondering what UDP is even used for as it seems to lack some critical features. Think real time applications like voice and video streaming, it uses UDP, if some data is lost there are no retransmission, they just move on and continue. 

| TCP                      | UDP                                   |
| ------------------------ | ------------------------------------- |
| Additional Features      | Lightweight                           |
| Connection Oriented      | Connectionless                        |
| Error Recovery(reliable) | Does not care about error(unreliable) |
| Windowing                | good for real time streaming          |
| Ordered Data Delivery    | DNS                                   |

UDP is lightweight, smaller headers, no retransmissions and no flow control. 

TCP has full feature set, application that would rather leave these details up to network stack. 

**Summary**

1. **Transport** Layer aims to getting information form one application to another 
2. It has TCP and UDP
3. The **port** is used to **identify** the applications on each device
4. **multiplexing**. It is a way that one host to have several applications accessing the network at one.
5. socket has local IP, local Port and Protocol.
6. **5-tuple** has two more: remote IP and remote Port
7.  TCP vs UDP
8.  **windowing**. It is where both sides of conversation agree on how much data can be send at once

### 8. Establishing Connections with TCP

TCP is a feature-rich transport protocol and the one that forms connections. TCP is connection-oriented. 

establishing connections means a device will start a connection to another device, they will agree to form a connection and set up parameters like port and sequence numbers. 

Three way handshake.

To do this it uses flags in TCP header. Flags are bits that maybe turned on or off. The device that starts the conversation is client. It sends a segment to server, there is no payload in this segment, just headers. In TCP header, the SYN flag is turned, it tells the server that we want to start a new connection and need to agree on few details. The first of details are the source and destinations ports. The source port will be random and destination will be well known number. The initial sequence number is also set,this help bot devices keep track of which all of the segments should be processed in, this usually starts as a randomized value.  Server has the first message, he can decide if it wants to be in this conversation. If it has an application listening on port 80, then it will indeed agree on this conversation. So it will response by sending an empty TCP. In TCP header, the source and destination will switch. The sequence number will go up by 1. SYN and ACK flags are both set. The client sends and empty TCP segment with the ACK and sequence number is increased again. This is the client confirming that it received the server's last message. 



Two ways to close connection

client sends TCP segment with FIN/ACK flags. server replay with ACK. follow up with FIN/ACK, then the client send back ACK.

why two pairs of same set of messages?

The firs pair announces and acknowedge the intention to close. The response now needs to notify the application that the connection is closing. It might take a few seconds for the application to deal with. The second pair of message are send only when the application is ready. It will send only when the application is ready. 

Using two pair messages will give the application time to respond before the connection is fully closed. 



Second way is send RST message.

**Summary**:

1. Three way handshake: SYN --- SYN/ACK --- ACK.
2. Four way farewell: FIN/ACK --- ACK --- FIN/ACK --- ACK
3. Another way farewell: RST (used for troubleshooting)
4. why two pairs:  give the application time to respond before the connection is fully closed. 

### 9. TCP Error Handling and Flow Control

Data can be lost for so many reasons. These errors are generally detected by the datalink protocol like Ethernet which will drop bad frames. Both TCP and UDP have error handling. They can detect corruption by using **value in checksum field.** but only TCP is considered reliable. This is because it will manage retransmission of the lost data. UDP on the other hand is considered unreliable as it will not try to recover from data loss. 

To understand how it works we must first look at how the segments are acknowledged you will remember that when a segment is received, the receiver sends an acknowledgement message confirming that it got the data. In the last video we saw that there are sequence numbers in the TCP header. One function of this is to reassemble the segments into the correct order but they also affect acknowledgments. Think of three way handshake. 

The sequence number track not the number of segments but the number of bytes being transferred. The advantage of this is when data went missing, there would be no acknowledgement for that range of bytes, the sender could then resend that range of data. But this is not very efficient to send an acknowledgement for every single segment. The sender would need to stop sending and wait for the ACK message before sending the next segment. The receiver would also need to spend more compute power generating these messages. So to make it more efficient TCP uses a process called **Windowing**. The allows the sender to send a certain amount of data, usually over multiple segments and the receiver send one single ACK to cover all of them. 

The amount of data that can be acknowledged in a single message is called the window size. This value is stored in the window field of the TCP header. 

Error control: Selective Acknowledgement(**SACK**). Does not need to resend all the segments. TCP used error recovery but UDP does not. If error are becoming frequent, TCP can adapt with the type of **flow control. What it will do is dynamically change the window size.**  

The three way handshake will set the port number, ISN(Initial Sequence Number) and window size, the window size is the amount of data a device can send before requiring an acknowledgement. But the window size is not just set between two devices, it's set for each connection and each connection can have a different size. Each connection can change over time too, which is why it's often called **sliding window**. The point is the receiver can tell the sender to send more or less information per acknowledgement. 

When the connection starts, they don't know how reliable the connection is. To deal with this they may start with a relatively small window size, If it's a reliable connection with very little or no data loss they may decide to increase maximum window size. A receiver can also use windows to signal the sender that's overwhelmed, it could set the window size to 0 which will effectively pause the sender giving the receiver time to catch up. 

**Summary**

1. Both TCP and UDP have error handling. They can detect corruption by using **value in checksum field.**
2. The sequence number track the number of bytes(not segments) being transferred
3. TCP error control: Selective Acknowledgement(SACK). uses **flow control** dynamically change the window size. 
4. The window size can change each connection, called **sliding window**.

### Questions

What happens when you type google in browser?

1. The browser DNS record to find the corresponding IP address.
2. The browser initiates a TCP connection with the server

DNS(Domain Name System) is a database that maintains the name of the website (URL) and the particular IP address it links to

DNS is a list of URLs, and their IP addresses, like how a phone book is a list of names and their corresponding phone numbers.



What is URL and URI?

URL: Uniform Resource Locator,  是网页地址

URI: Uniform Resource Identifier, 表示可标识的对象

a URI can be a name, locator, or both for an online resource where a URL is just the locator. URI >> URL.





#### Basic

Application layer: interaction between process: DNS, HTTP, SMTP

DNS Domain Name System is a mapping between IP address and domain names

transport layer: data transport service

UDP: User Datagram Protocol: provide no connection, unreliable transport service

Network layer: choose right router and swith node, ensure data transmission

![七层体系结构图](https://camo.githubusercontent.com/62a81cdf1d9840226e1a49625e5821f17e655cfd/68747470733a2f2f6d792d626c6f672d746f2d7573652e6f73732d636e2d6265696a696e672e616c6979756e63732e636f6d2f323031392f372f2545342542382538332545352542312538322545342542442539332545372542332542422545372542422539332545362539452538342545352539422542452e706e67)

Why is TCP reliable:

1. Flow control: it has buffer space, if the buffer is full, reduce sending rate
2. Congestion control: When the network is congested, reduce data transmission
3. Retransmit after timeout

What happens when you type URL?

1. DNS resolution
2. TCP connection
3. Send HTTP request
4. The server processes the request and returns an HTTP message
5. The browser parses the rendered page
6. End of connection