# 计算机网络

> * LAN 局域网
> * WAN  广域网
> * Router 路由器
> * Switch 交换机
> * Protocol 协议
> * Packet 分组/报文/数据包
> * ISP 因特网服务提供商
> * TCP 传输控制协议
> * UDP 用户数据报协议
> * Intranet 内网
> * Bandwidth 带宽
> * infrastructure 基础设施
> * Ethernet 以太网
> * Multiplexing 多路复用
> * Encapsulation 封装
> * Stack 栈
> * FDM 频分复用
> * TDM 时分复用
> * congestion 拥挤拥塞
> * Extranet 外网
> * NIC Network interface card
> * Modem
> * Topology
> * Throughput(吞吐量)

### 网络的划分

#### 网络的Topology结构

##### (总线)Bus Topology 

all the devices on a bus topology are connected by one single cable 

> 末端要加适配电阻

##### (环)Ring Topology

Single single cable

Dual both diirections

##### (星)Star Topology

Star & Tree Topology 
most used architecture in Ethernet LANs

##### Extended Star Topology

Larger networks

##### (混合) Mesh Topology

#### 按照scale(规模)划分

LAN (Local Area Network)

WAN (World Area Network)

Internet 

MAN (Metropolitan Area Network)

#### Classefied by boundary

Intranet (private Networks)

Extranet (public Networks)

###什么是Internet

> Internet standards :
> RFC:Request for comments
> IETF:Internet Engineering Task Force

#### 从具体构成描述。
因特网是世界范围的计算机网络 即网络的网络

define:

> (网络边界) network edge: 
> ​	applications and hosts
> access networks physical media:
> ​	wired ,wireless ,communication links
> (网络核心)network core:
> ​	interconnected routers,network of networks

service view 

>communication infrastructure : enables distributed applications
>communication services provided to apps:
>connection-oriented reliable

### Internet History

* 1961: packet-switching
* 1964:Baran-packet-switching in military nets
* 1967:ARPAnet conceived
* 1969:first ARPAnet node
* 1972:

  * ARPAnet public demonstration

  * NCP (Network Control Protocol) host-host(端到端)

  * first e-mail program

  * ARPAnet has 15 nodes
* 1970:ALOHAnet satellite network Hawaii
* 1974:interconnecting networks
* 1976:Ethernet at Xerox PARC
* ate 70's proprietary architectures:DECnet SNA XNA
* late70's switching fixed length packets (ATM)

> Cerf and Kahn’s internetworking principles:
>
> nminimalism, autonomy - no internal changes required to interconnectnetworks
>
> nbest effort service model
>
> nstateless routers
>
> ndecentralized control

* 1983: deployment of TCP/IP
* 1982: smtp e-mail protocol defined 
* 1983: DNS defined forname-to-IP-address translation
* 1985: ftp protocol defined
* 1988: TCP congestion control

.....

### Network edge

* network edge : applications and hosts 
* network core :routers network of networks
* access networks ,physical media: communication links
* end systems(hosts)
  * run application programs
* client/server model
* peer-peer model
  * minimal use od dedicated servers

## Circuit Switching: FDM and TDM

频率划分 时域划分

时分复用

需要建立连接

### Packet Switching

> hop 单步
> statistical multiplexing 统计多路复用
> cable modems 电缆调制解调器
> headend 前端
> HFC 混合光线同轴电缆

ADSL
FTTx
Residential access:cable modems
Enterprise Network Access:local area networks(Ethernet)



### Physical Media

* Bit 

* physical link

* guided media

* unguided media

  ​

  TP 双绞线

  UTP 无屏蔽双绞线 STP 屏蔽双绞线

### Performance of Computer network

Date rate (数据率)
Bandwidth(带宽)
Throughput(吞吐量)

### Four sources of packet delay

d_nodal = d+_proc + d_queue + d_trans + d_prop

processing 处理
propagation 传播

### Internet structure

没有中心

Tier-1 ISP 互联网提供商
NAP (network access points)
Tier-2 ISP 
Tier-3 ISPs and local ISPs (last hop "access" network closest to end systems)

CRC?

Internet 中不能轻易定义 数据包网络是面向有链接还是无连接的

# Link Layer

> hosts and routers -> nodes
> packet is frame
> layer-2 packet is frame

EDC = Error Detection and Correction bits

### Parity Checking

### Internet checksum

### CRC Cyclic Redundancy Check

802.11??

### Multiple Access Links and Protocols

* point-to-point
  * PPP for dial-up access
  * point-to-point link between Ethernet switch
* broadcast
  * traditional Ethernet
  * upstream HFC
  * 802.11 wireless LAN

single shared broadcast channel
two or more simultaneous transmissions by nodes:interference
distributed algorithm that determines how nodes share channel .... determine when node can transmit
communication about channel sharing must use channel itself

distributed  分布式

### MAC protocols

信道划分

* TDMA 时序划分
* 频率划分

随机访问

(时隙ALOHA )Slotted ALOHA

* 假设 所有frames 大小相同 
* 时间被划分为相等的时隙 传输1帧时间
* 节点同步
* 所有节点都能检测冲突

Pure (unslotted) ALOHA

no synchronization

CSMA (Carrier Sense Multiple Access)

* CSMA: listen before transmit

CSMA/CD (Collision Detection)

 ### LAN 

#### MAC Addresses and ARP

IP 32
MAC 48bit

CASM/CD efficiency=1/(1+5t_prop/t_trans)

争用期
：两倍端到端往返时延

5-4-3-2-1