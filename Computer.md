## Shell

### 1. Shell是什么

1. 是一个程序，提供内核与用户对话的环境: User --- Shell --- Kernel
2. 命令解释器，可以写出各种script.
3. 工具箱

Bash 是目前最常用的 Shell，基本可以相等

### 2. 常用命令

`echo` 是在屏幕上输出一行文本， 如果想要输出的是多行文本，即包括换行符。这时需要把多行文本放在引号里面。

`-n`取消末尾的回车符，可以让两个`echo`输出连在一起

`-e`参数会解释引号（双引号和单引号）里面的特殊字符

```bash
$ echo "Hello\nWorld"
Hello\nWorld
# 将换行符解释出来
$ echo -e "Hello\nWorld"
Hello
World
```

Shell组成：由命令和参数组成，参数前的 -l 和 --list 作用相同，一般用短的便于输入

多行命令：在每一行的结尾加上反斜杠`\`，和下一行一起解释

空格区分参数，自动忽略多余的空格

分号（`;`）是命令的结束符，使得一行可以放置多个命令，上一个命令执行结束后，再执行第二个命令

```bash
# 如果1运行成功，继续运行2
Command1 && Command2 
# 如果1运行失败，继续运行2
Command1 || Command2
```

`type`命令用来判断命令的来源: 内置命令或者外部程序

### 3.八种拓展

Shell 接收到用户输入的命令以后，会根据空格将用户的输入，拆分成一个个词元（token）。然后，Shell 会扩展词元里面的特殊字符，扩展完成后才会调用相应的命令 ： 命令---词元---扩展---调用

```bash
$ set -f # 关闭扩展
$ set +f # 打开扩展
```

#### 

`~`会自动扩展成当前用户的主目录

`~+`会扩展成当前所在的目录，等同于`pwd`命令

`?`字符代表文件路径里面的任意单个字符，不包括空字符

`*`字符代表文件路径里面任意数量的任意字符，包括零个字符

不包含隐藏文件，只匹配当前目录，不匹配子目录

`[]`匹配方括号之中任意一个字符

`[!]`或者`[°]`匹配不在方括号里面的字符

`[start-end]`匹配连续的范围，例如`[1-9]`

`{}`表示分别扩展成大括号里面的所有值，用逗号分隔

`{start-end}`扩展成连续序列，支持逆序



### Sed

sed是一种流编辑器，一次处理一行。处理时，把当前处理的行存储在临时缓冲区，完成后把内容送往屏幕，再处理下一行。

基本用法 sed [] 'command' filename

| 参数 | 功能                                |
| ---- | ----------------------------------- |
| -e   | 直接在指令列模式上进行sed的动作编辑 |

| 命令 | 功能       |
| ---- | ---------- |
| a    | 新增       |
| d    | 删除       |
| s    | 查找并替换 |



NF is for the number of fields in the current record. 列数
NR is for the number of records in the input file. 行数



## Network

What is network?

network: connect devices / devices share information

### 1. Introduction

#### 1.1 What are the two ways computers can connect to the network?

wireless --- WIFI (device: Access Point)

cable --- Ethernet (device: switch)

#### 1.2 Difference between LAN and WAN?

LAN: Local Area Network, a network in a local area

WAN: Wide Area Network, connect networks that are separated. Can call enterprise network.

### 2. Cabling Devices

#### 2.1 Difference between MAC and IP?

MAC (Media Access Control) : unique, used **within** a LAN segment.

IP (Internet protocol): access hosts on a **different** LAN segment.

#### 2.2 How many MAC address does a computer have?

Computer can have have multiple MAC Addresses**, **one  for each Network interface

### 3. OSI Model

The goal of OSI model is to allow different protocols and vendors to work together. 

| Capital | Layer        | Example   | Function                                                     |
| ------- | ------------ | --------- | ------------------------------------------------------------ |
| Please  | Physical     | Ethernet  | manage physical components, encode data                      |
| Do      | Data Link    | Ethernet  | create logical link between devices, add local address       |
| Not     | Network      | TCP / UDP | choose right router and switch nodes, ensure data transmission |
| Throw   | Transport    | IP        | transport data between applications                          |
| Sausage | Session      |           | create session between applications                          |
| Pizza   | Presentation |           | data conversion and format                                   |
| Away    | Application  |           | access network                                               |

<img src="https://camo.githubusercontent.com/62a81cdf1d9840226e1a49625e5821f17e655cfd/68747470733a2f2f6d792d626c6f672d746f2d7573652e6f73732d636e2d6265696a696e672e616c6979756e63732e636f6d2f323031392f372f2545342542382538332545352542312538322545342542442539332545372542332542422545372542422539332545362539452538342545352539422542452e706e67" alt="七层体系结构图" style="zoom: 67%;" />



### 4. IP Address

#### 4.1 What is IP address?

IP address are two address in on: Host Address + Network Address

| IP   | Belongs to | IP Bit    |
| ---- | ---------- | --------- |
| 192  | Network    | 1100 0000 |
| 168  | Network    | 1010 1000 |
| 0    | Host       | 0000 0000 |
| 100  | Host       | 0110 0100 |

#### 4.2 How many classes do IP address have?

| Class | Octets                                                       | Range                     |
| ----- | ------------------------------------------------------------ | ------------------------- |
| A     | Device, 1 Octet - 1 bit = 7 bits<br /> 128 Networks, 16M Hosts | 1.0.0.0-126.0.0.0         |
| B     | Device, 2 Octets - 2 bits= 14 bits <br />16T Networks, 65T Hosts | 128.0.0.0-191.255.0.0     |
| C     | Device, 3 Octets - 3 bits=21bits <br />2M Networks, 255 Hosts | 192.0.0.0-223.255.255.0   |
| D     | Multicast                                                    | 224.0.0.0-239.255.255.255 |
| E     | Reserved                                                     |                           |

#### 4.3 What is subnet mask? 

break large network into small ones

172.16.1.0/24   24 means first 24 bits are used for network

#### 4.4 How to have more session at the same time?

The combination of IP and port number enable system to have more than one session open at a time and track them.

### 5. TCP / UDP

#### 5.1 What is port?

The port are used to **identify** the applications on each device

#### 5.2 What is multiplexing?

 *It is a way that one host to have several applications accessing the network at one.* They all share the one network card the one network stack the one IP address but they each use different ports. 

#### 5.3 What is socket?

A network application uses a concept called **socket**, it made up of a local IP address, a local port number and a protocol. As port numbers are unique so are sockets. Therefore, a socket can identify which application the network data belongs to. 

| Local IP   | Local Port | Protocol |
| ---------- | ---------- | -------- |
| 172.16.0.1 | 80         | TCP      |

#### 5.4 What is windowing(TCP)?

It also leads into a TCP feature called **windowing**. It is where both sides of conversation agree on how much data can be send at once before the receiver to acknowledge. It's value is called window size. If there is no data loss, the window size can dynamically grow if there is data loss, the window size will dynamically shrink. 

#### 5.5 Why is TCP reliable?

1. Flow control: it has buffer space, if the buffer is full, reduce sending rate
2. Congestion control: When the network is congested, reduce data transmission
3. Retransmit after timeout

#### 5.6 Difference between TCP and UDP

| TCP                      | UDP                                   |
| ------------------------ | ------------------------------------- |
| Additional Features      | Lightweight                           |
| Connection Oriented      | Connectionless                        |
| Error Recovery(reliable) | Does not care about error(unreliable) |
| Windowing                | good for real time streaming          |
| Ordered Data Delivery    | DNS                                   |

#### 5.7 TCP Connections

1. Three way handshake: SYN --- SYN/ACK --- ACK.
2. Four way farewell: FIN/ACK --- ACK --- FIN/ACK --- ACK
3. Another way farewell: RST (used for troubleshooting)
4. why two pairs:  give the application time to respond before the connection is fully closed. 

<img src="https://miro.medium.com/max/805/0*WcbPv9sWlCl6RV4a" alt="What is tcp three way handshake ? What is SYN , ACK packets ? | by ..." style="zoom:50%;" />

#### 5.8 TCP Error Handling & Flow Control

1. Both TCP and UDP have error handling. They can detect corruption by using **value in checksum field.**
2. The sequence number track the number of **bytes**(not segments) being transferred
3. TCP error control: Selective Acknowledgement(SACK). uses **flow control** dynamically change the window size. 
4. The window size can change each connection, called **sliding window**.

### 6. Questions

####  6.1 What is DNS?

DNS(Domain Name System) is a database that maintains the name of the website (URL) and the particular IP address it links to

DNS is a list of URLs, and their IP addresses, like how a phone book is a list of names and their corresponding phone numbers.

#### 6.2 What happens when you type URL?

1. DNS resolution
2. TCP connection
3. Send HTTP request
4. The server processes the request and returns an HTTP message
5. The browser parses the rendered page
6. End of connection

#### 6.3 Difference between URL and URI?

URL: Uniform Resource Locator,  是网页地址

URI: Uniform Resource Identifier, 表示可标识的对象

a URI can be a name, locator, or both for an online resource where a URL is just the locator. URI >> URL.



