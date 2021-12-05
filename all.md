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
- Dependant on transmission rate (bps) or bandwith
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

<hr />

## Week 2

### Tasks in networking
What does it take to send packets across
- Prepare data (Application)
- Ensure packets get to the dst process (Transport)
- Deliver packets across global network (Network)
- Delivery packets within local network to next hop (Datalink)

Internet protocol stack
- application: support network applications (HTTP SMTP)
- transport: process-process data transfer (TCP, UDP)
- network: routing of datagrams from source to destination (IP, routing protocols)
- link: data transfer between neighboring network elements (Ethernet, WiFi, PPP)
- physical: bts "on the wire"

Three Observations:
Each layer depends on the layer below
- supports the layer above
- independent of others
- There are multiple versions of a layer (TCP, UDP) depending on what is being done
- There is only one IP layer

- layering is good for extension and creation of new applications, otherwise each new application would need to be **re-implemented** for every network technology
- Introducing an intermediate layer provides a **common** abstraction for various network technologies
- makes it easy to introduce new protocols
- prevents technology from one layer affecting another layer

cons of layering:
Layers may duplicate lower-level functionality
information hiding may hurt performance
headers start to get large
layer violations when the gains too great to resist
layer violations when network doesn't trust ends

Routers - l3 packet switches
Switches (link layer switches, bridges) - l2 packet switches
Hosts - applications generate data/messages

<hr />

#### Application Layer:
- Web & HTTP, electronic email (SMTP)
- write programs that run on different end systems
- communicate over network
- no need to write software for network core devices
- network-core devices do not run user applications
- applications on end systems allow for rapid app development, propogation

**Client-server paradigm**
Server:
- always-on host
- permanent IP address
- datacenters for scaling

Clients:
- contanct, communicate with server
- may be intermittently connected
- may have dynamic IP addresses
- do not communicate directly with each other
- HTTP, IMAP, FTP

**Peer-peer architecture**
- end systems directly communicate
- peers request and provide service to other peers
- self scalability (each peer brings new service capacity)

**Prcesses Communicating**
A program running within a host
- within same host, two processes communicate using inter-process communication (defined by OS)
- processes in different hosts communicate by exchanging **messages**

**Sockets**
- doorways in which processes send messages to eachother
- proces sends/recieves messages to/from its socket
- socket analogous to door
- sending process shoves message out the door
- sending process relies on transport infrastructure on other side of door to deliver message to socket at receving process
- two sockets (one on each side)

#### Application layer protocol defines:
- Types of messages exchanged (request, response)
- message syntax (what fields in messages & how fields are delineated)
- message semantics (meaning of information in fields)
- rules

**open protocols**
- HTTP, SMPT, WebRTC
- defined in RFCs, everyone has access to protocol definition

**propietary protocols** (not open source)
- Skype, Zoom, Teams


#### Application Layer: Web & HTTP (Hypertext Transport Protocol)
- Web page consists of objects, each of which can be stored on different Web servers
- object can be HTML file, JPEG image, Java applet, audio file
- web page consists of base **HTML-file** which includes **several referenced objects** each addressable by a **URL**

e.g **www.someschool.edu**/someDept/pic.gif
the bold part is the host name, and the latter is the path name of the file(s)

**URL** (Uniform Resource Locator)
protocol://host-name[:port]/directory-path/resource
- protocol: http, ftp, https, smtp etc.
- hostname: **DNS name**, IP address
- port
- directory path & resource

HTTP Overview
- Web aplication layer protocol
- Client/server model
    -   Client: browser that requests, recieves (using HTTP protocols) and displays Web objects
    -   Server: Web server sends (using HTTP protocol) objects in response to requests
- HTTP uses TCP (since its more reliable)
    - client initiates TCP connection
- HTTP is "stateless"

**HTTP REQUEST METHODS**
- POST (web page often includes form input)
- GET sending data to server
- HEAD requests headers only, that would be returned if specified URL were requested with an HTTP GET method
- PUT uploads new file (object) to the server, completely replaces file that exists at specified URL with content in entity body of POST HTTP request message

**HTTP response status codes**
- 200 OK (request suceeded)
- 301 Moved permanently, requested object moved, new location specified later in this message (300 redirection)
- 400 Bad request (request msg not understood by server) (400 errors)
- 505 HTTPVersion not supported

**Cookies (Maintaining user/server state)**
- HTTP GET/response interaction is **stateless**
- Cookies are used to maintain some state between transactions

Cookies components:
1) Cookie header line of HTTP response message
2) Cookie header line in next HHTP reqest message
3) Cookie file kept on yser's host, managed by user's browser
4) backend database at Web site


**HTTP Performance**
- Page Load Time (PLT) Measures web performance
- Dependant on tha amount of content/structure/protocols and network bandwith


#### Transport layer

What transport service does an app need?
- data integrity (reliable data transfer depending on application)
- timing (some apps require low delay to be effective)
- throughput
- security

**Internet transport protocols services**

##### TCP
- reliable transport between sending and receiving processes
- flow control: sender does not overwhelm the receiver
- congestion control: throttle sender when network overloaded
- does not provide: timing, minimum throughput gaurantee, security
- connection-oriented: setup required
- cannot control the rate to push data
##### UDP
- unreliable data transfer between sending and receiving process
- does not provide: reliability, flow, control, congestion control, timing, throughput gaurantee, security or connection setup.
- can push out data at whatever rate want (more control)

<hr />

#### DNS

##### Overview:
DNS is usefull in such a way that we can use words or phrases to access inforamtion online (via domain names: e.g google.com). This is useful because servers actually use ip addresses.
Which is extremely difficult for humans to interpret/remember.

So how does your computer get the appropiate ip address from the domain name?

###### Local Cache:
Your computer/browser has a local cache of any domains previously accessed, saving all relevant information such as the IP address for future use to improve loading time.

Otherwise if no entries are found for the associated domain name, it must go through a DNS recursive resolver

###### DNS recursive resolver
- Computer sends a query to a DNS resolver (usually managed by ISP) asking for an IP address for the domain name
- This DNS resolver has its own seperate cache, which similarly stores any DNS entries and their associated IP addresses.
- If an entry is found in its cache, it sends back the IP address to the requesting device, which the device can then communicate directly with the IP address.

1. Otherwise if the DNS is not found in the cache, it sends a request to a ROOT name server (Top of the DNS hierarchy, provides details of the top level domain servers)
2. ROOT server refers us to top level domain server (e.g. .com), which is then queried again by the DNS resolver (TLD - contains information for domains with a specific extension .com .org .net)'
3. TLD knows the location of the authoritative name server, which is sent back to the resolver so that the resolver can then query the authoritative name server.
4. After querying the authoritative name server, the resolver should then hopefully have the associated IP address for the specified domain name. (Authoritative name server is the last step)

Root NS -> TLD NS -> Authoritative NS 

![dns process](https://www.cloudflare.com/img/learning/dns/what-is-dns/dns-lookup-diagram.png)