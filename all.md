# COMP 3331 Notes 21T3
<hr />

### Course Content
- Introductory course in computer networking
- Principles and practice of computer networking
- **Internet**

How the internet works:
- internet is a complex global infrastructure
- organising principles of the internet
- what really happens when you browse the web
- TCP/IP, DNS, HTTP, NAT, VPNs... (Protocols)

Fundamentals of computer networks
- design strategies
- evaluate network performance (performance centric)

<hr />

## Week 1

### What is the Internet?
- The internet is an infrastructure that provides services to networked applications
- An interconnection of different computer networks

Components of the internet:
- Billions of connected computing **devices** with hosts as the end systems, running network apps at the Internet's "edge"
- hosts primarily run network applications "Host network applications"
- **Packet switches** forward packets (chunks of data), routers switches
- **Communication links**, cable (fibre,copper) or radio/satellite. transmission rate: bandwith
- **Networks** = collection of devices, routers, links: managed by an organization.

Internet = network of networks (interconnected Internet service providers)
Protocols = control sending, receiving of messages/data (HTTP, Streaming, Skype, Wifi...)
Internet Standards = RFC: Request for comments, IETF, Internet Engineering Task Force

Internet as a "Service":
- **Infrastructure** provides services to applications (Web, multimedia streaming, emails)
- provides a **programming interface** to distributed applications.
- "hooks" allowing sending/receiving apps to "connect" to, use internet transport service
- provides service options, analogoous to postal service

### What are protocols?
Think of protocols as the action of receiving a message and conducting an action based on that message.

All communication activity on the internet are governed by protocols
- define the format, order of messages sent and received among network entities.

Example of a protocol in networks
1. TCP connection request from the device
2. TCP connection response from the server
3. GET request from device for the webpage
4. Content displayed to the device from the server

### Network edge: hosts, access network, physical media
Network edge:
- Hosts: clients and servers
- servers are often in data centers

Access Networks, physical media:
- networks that allow end systems to connect to the internet
- wired, wireless communication links

Network core:
- interconnected routers
- network of networks

Access networks: digital subscriber line (DSL)
- using existing telephone line to central office DSLAM
DSLAM = DSL Access multiplexer, Aggregates all the traffic

Closer you are to DSLAM the higher the data rate you can get

ADSL frequency/bandwith
- Channel reserved for telephone line (smallest) PSTN - public switch telephone network
- Channel reserved for Upstream (upload, close second in smallest)
- Channel reserved for Downstream (download, majority usually)
- bandwith is not shared

Cable based access
- HFC
- **network** of cable, fiber attaches hopes to ISP router
- homes **share access netowrk** to cable end, which can lead to slower rates when under large load
- bandwith is shared

Fibre:
- Fully optical fibre path all the way to the home
- NBN, Google
- 30 Mbps to 1 Gbps
- bandwith is not shared

### Wireless access networks
Shared wireless access network connecting end systems to router
- Wireless local area networks (WLANs) or WiFi
- Wide-area cellular access networks - for wider areas (in km), 4G, 5G used in phones

### Enterprise networks
- Companies, uni
- mix of wired, wireless link technologies, connecting a mix of switches and routers
- high speeds

<hr />

### Network Core: Packet/circuit switching
Packet-Switching (What we currently use):
- hosts break application-layer messages into packets
- packets are forwarded from one router to the next, across links from the source to destination
- each packet transmitted at full link capacity
- Data is sent as chunks of formatted bits (Packets)
- Packets consist of a "header" and "payload"
- header = controlled information to send to the network (internet address, Age/TTL, CheckSum)
- payload = actual data (split up into packets)
- Store and forward switching = switch processes/forwards a packet after it has been recieved fully.
- Cut through switch can reduce delays. 
- Each packet travels independently (lookups happen independently regardless of the previous packet).
- No link resources are reserved, packet switching leverages statistical multiplexing.
- allows more useres to use the network
- probability that the number of active users > 10 = 0.0004 (in a network of 35 users approx ~ calc using binomial)
- resources are allocated on demand
#### Binomial Probability Distribution
- Fixed number of observations (trails), n
- Binary random variable
- Constant probability for each observation


#### Peek ahead: Two key network-core functions
- What a router does
Forwarding:
- local action: move arriving packets from router's input link to appropiate router output link
Routing:
- global action determine source-destination paths taken by packets
- routing algorithms


Circuit-Switching:
- Alternative used in legacy telephone networks was considered during the design of the internet
- FDM and TDM
- FDM = Frequency division multiplexing (electromagnetic frequencies divided into narrow frequency bands)
- TDM = Time division Multiplexing (Time dividided into slots)
- inefficient (bursty communication patterns)/ non scalable
- fixed data rates
- connection state maintenance
- limit to sharing total capacity
- less users can use the network
- resources are provisioned right from the start (reservations need to be made)
- packets travel the same path in the same link



#### Timing in packet switching (Store and forward):
- Packet switch processes/forwards a packet after it is recieved entirely
- each packet travels independently
- no link resources are reserved (using statistical multiplexing)
- Statisical multiplexing relies on the assumption that not all flows burst at the same time

#### Bursts in Traffic & overload:
- To combat overloaded capacity, we use statistical multiplexing
- When the capcity is overloaded (to much data at once):
- **Transient Overload**: Two links are sending data to a packet switch, where packets from both links are recieved at the same time
- To combat a **Transient Overload** is to queue the overload into a packet buffer.
- **Persistent overload**, infinite overload from 2 or more links, the queue size in the buffer is limited, hence packets will eventually be dropped

#### Packet's pros and cons:
- Packet is great for "bursty" data (not always sending)
- Packet is simpler with no call setup and great for resource sharing
- Congestion is possible, resulting in packet delay/loss due to buffer overflow
- Protocols needed for reliable data transfer, congestion control
- bandwith guarantees traditionally used for audio/video applications

<hr />

### Internet Structure: a "network of networks"
- Hosts connect to Internet via **access** ISPs (residential, enterprise)
- Access ISPs must be interconnected (any two hosts can send packets to eachother)
- Resulting network of networks is very complex
- Access networks are connected to regional ISPs then to larger global ISP's which then these ISP's are connected to eachother on a global scale
- Global ISPs connected through IXP (Internet exchange point)
- Content provider networks (google, facebook): private network connecting their data centers to Internet, bypassing teir-1 regional ISPs


#### Performance: loss, delay, throughput
- arrival rate to link temporarily exceeds output link capacity: packet loss
- packets queue in router buffers, if full, can lead to packet loss/delay
- **transmission delay** packet being transmitted
- **packets in buffers** queueing delay
- free (available) buffers: arriving packets
- dropped (loss) if no free buffers
- Four sources of packet delay **transmission**, **propogation**, **nodal processing**, **queueing**


#### nodal processing:
- check bit errors
- determine output link
- as low as nanoseconds

#### queueing delay:
- time waiting at output link for transmission
- dependant on congestion level of the router

#### transmission delay
- Dependant on packet length (bits)
- Dependant on transmission rate (bps)
- d_trans = packet length / transmission rate

#### propogation delay:
- length of physical link (d)
- propogation speed (s)
- d_prop = d/s
- think of real world physics

#### throughput:
- rate that bits are sent from sender to receiver (end to end)
- instantaneous rate: rate at a given point in time
- average: rate over a longer period of time
- often bottlenecks (links)


