# Computer Networks

Remember kbps is kilo bits, kBps is kilobytes

# Section 1: 
## Section 1.1
### The internet: a "nuts and bolts" view

Billions of connected computing devices
* **hosts** = end systems
* running network apps at internet's "edge" 

Packet switches: forward packets (chunks of data) (moves packets)
* routers, switches

Communication links
* fiber, copper, radio, satellite
* Transimission rate is called the bandwidth

Networks
* Collections of devices, routers, links managed by an organization.

Internet: "network of networks"
* Interconnected internet service providers (ISP)

Protocols are everywhere
* which control sending, receiving of messages
* Example: HTTP(Web), streaming video, Skype, TCP, IP, Ethernet, WiFi, 4G

Internet standards (who define the protocols)
* RFC: Request for Comments
* IETF: Internet Engineering Task Force

### The Internet: a "services" view

Infrastructure that provides services to applications:
* Web, streaming video, email, games, e-commerce ...
  
Provides programming interface to distributed applications:
* *hooks* allowing sending/receiving apps to *connect* to, use the internet transport service
* provides service options, analogous to postal service  

## Section 1.2


Frequency division multiplexing used in cables as well to send data on different frequenies.

## Section 1.3

### **Packet switching**

* Hosts break application layer messages into packets. 
* The network forwards packet from one router to the next, across links on path from source to destination.

**Forwarding** is a local action in the router, which looks up where the pack is going through a table.

**Routing** is a global action that routes the packet to the destination.

![alt text](image.png)

* store and forward approach. 
* Queueing, when packets come faster than it can send. if the buffer is filled then packets can be lost.

* Great for bursty data

### **Circuit switching**

* Reseverd end to end resources.
* Great for continuous data.
* FDM AND TDM

## Section 1.4

![alt text](image-3.png)
![alt text](image-4.png)
![alt text](image-5.png)

### Throughput

* Rate at awhich bits are being sent from sender to receiver. Can be instantaneous or average. 
* **Bottleneck link** is the link on the end to end path that constrains the end to end throughput
* Always consider the bottleneck or the smallest bit rate for the throughput value.
* **Time = filesize/throughput**
![alt text](image-8.png)

## Section 1.5

![alt text](image-6.png)
![alt text](image-7.png)

* Transport layer encapsulates the application layer message M with a transport layer-layer header H_t to create a transport layer **segment**.
* Network layer encapsulates the transport layer segment [H_t | M] with a network layer-layer header H_n to create a network layer **datagram**.
* Link layer encapsulates the Link layer segment [H_n | H_t | M] with a link layer-layer header H_l to create a link layer **frame**.

## Section 1.6

### Bad attackers 

* Packet sniffing: shared network, can access everything once they are on the network.
* IP spoofing: injection of packet with false source address.
* Denial of Service (DoS): overwhelming the host by sending loads of packets.

### Lines of defence
* Authentication
* confidentiality
* integrtity checks
* access restrictions
* firewalls

## Section 1.7 

# Section 2: Application Layer

## Section 2.1: Principles of Network Applications

### Client-server 
**Server**
* always on host
* permanent IP address
* In data centers for scaling

**Client**
* Communicates with the server
* May be intermittenly connected
* can have dynamic ip address
* do not communicate with directly with each other(client)
* examples: HTTP, IMAP, FTP

### Peer-peer
*  doesnt have always on servers
*  peers request and provide services from other peers
   *  Adds to self scalability
*  Peers are intermittenly connected and change IP addresses
   *  Hard to manage 
*  Example: P2P file sharing
  
### Processes communicating

**Process** are programs running within a hosst

* In the same host, two processess communicaate using inter-process communication
* processes in differnet hosts communicate by exchaning messages

Process that initiates the communication is called the **client process**

Process that waits to be contacted is the **server process** 

### Sockets

* Process sends/receives messages to/from its socket
* Sockets can be thought of as doors
  * Sending process sends messages outdoor
  * sending process relies on the transport infrastructure
  * Two sockets involved: one on each side  

![alt text](image-1.png)

### Addressing process

* This is basically the address of the processes (door)
* To receive messages, the process must have an **identifier**
* Host device has unique 32-bit IP address
* Identifier includes both **IP addresses** and **port numbers**

### Application layer protocol defines:

RFC: Request for comments

* defines the type of messages exchanged
  * Request, response etc
* message syntax
  * what fields in the message and how fields are delineated
* message semantics
  * meaning of information in fields
* Rules for when and how processes send and respond to messages

Two types of protocols

* **Open protocols**
  * Defined in RFCs, everyone can access the definition
  * allows interoperability
  * example HTTP. SMTP
* **Proprietary protocols**
  * example: skype, zoom 

### What transport service does an app need

* Data Integrity
  * some apps require 100% reliable data transfer
  * example: file transfer, web transactions
  * Other apps like audio can tolerate some loss
* Timing
  * Some apps require low delay to be effective
* Throughput
  * Some apps require minimum amount of throughput to be effective 
  * other apps can make use of whatever they get (elastic)
* Security
  * encryption, data integrity

### Internet transport protocols services
![alt text](image-2.png)

## Section 2.2: Web and HTTP

* Web page consists of object that can be sotred on different web servers
* HTML file, image, audio
* URL
![alt text](image-9.png)

**HTTP**

* Hypertext transfer protocol.
* client server model
![alt text](image-10.png)
* uses tcp
* is stateless: doesnt maintain information about past

**Types of HTTP**
![alt text](image-11.png)

* Round trip time
![alt text](image-12.png)

![alt text](image-13.png)

### **HTTP protocol**

**Request**
![alt text](image-14.png)

![alt text](image-15.png)

**Response**
![alt text](image-16.png)

![alt text](image-17.png)

**Cookies**
![alt text](image-18.png)


## Section 2.2: HTTP

Caching servers reduces totoal time ti takes to get the object

Using conditional get to check the object is up to date

## Section 2.3: EMail

* Three components: users, email servers, smtp protocol 

### SMTP RFC
* uses TCP to send email message from cleient to server
* Three phases
  * smtp handshaking
  * smtp transfer of messages
  * smtg closure
* command/response interaction like http
  * commands: ascii text
  * response: status code and phrase

![alt text](image-19.png)

* As smtp is used to push data, there needs to be a protocl to receive this data called the IMAP

![alt text](image-20.png)

# 2.4 Domain name system

 * distributed database 
   * decentralized approach
     * makes it easy to scale
 * application layer protocol
 * DNS services
   * hostname to ip address translation
   * host aliasing
   * mail server alisaisng
   * load distribution
![alt text](image-21.png)

![alt text](image-22.png)

![alt text](image-23.png)

Iteration used a lot more than recursive


# Section 2.5 file transfer protocol

* Similar to HTTP
* uses TCP
* main difference is that ftp uses two parallel tcp connection to transfer a file, a control connection and data connection
* control connection: used to send control information between the two hosts, like passpord, file directorand commands like put and get files.
* data connection actaully sends the file. 
* FTP is out band as it uses separate control conenctions
* HTTP is in band as it uses the control connections in the same tcp connection

Basic working of ftp is it opens the control connection, sends and gets the relevant stuff, once its allowed to send or get the file, it opens another data connection to get/send the file and hten close the data channel. If wants to send another channel then another data channel will be opened.

* FTP must maintiain the state of the user. THe server must associate the control connection wit ha specific user account. HTTP is stateless

* commands to send like: USER, PASS (Passoword), LIST (list of all files), RETR (retureive the file, this causes a data channel conenection to open and send file), STOR (stroed the file)

* replies: 331 username ok , passowrd reuqired
* ....

## 2.6 Video streaming 

# Section 3: Transport layer

## 3.2 Multiplexing and demultiplexing

UDP and TCP have differet ways of doing it

* UDP only cares about hte senders and destination ports
* TCP is made up a 4 tuple of the ip and the port for sender and destination

### UDP

* bare bones
* best effort service
  * some segments may be lost, delevierd out of order
* connectionless
  * no handshaking 
  * each segmemnt is handled independently
  
**Checksum**

* add the two 16 bit numbers 
* do 1's complement of the sum and attach that as the checksum
* works for 1 bit error flip
* But not always for two bit error flip

## 3.4: Reliable data transfer

rdt 3.0: adds more sequence numbers and can send more packets at once which leads to pipelining


# Section 6: Link Layer

## Section 6.2: Error Detection and Correction Techniques

[Link for a simple example on CRC](https://www.youtube.com/watch?v=ZJH0KT6c0B0)

Key points:
- XOR used for subtraction in the division
- watch the video to know when to use 1 or 0 to get the remainder stuff.
