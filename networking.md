## Stack of the protocol
- Ajax -> Stateful
- HTTP -> Stateless
- TCP -> Sessionful
- IP -> Sessionless

## Other
- NAT: NAT stands for network address translation. 
It is a way to translate requests that are incoming into a routing server to the relevant devices or servers that it 
knows about in the LAN. This is usually implemented in physical LANs as a way to route requests through one IP address 
to the necessary backend servers.
- VPN: VPN stands for virtual private network. It is a means of connecting separate LANs through the internet, while 
maintaining privacy. This is used as a means of connecting remote systems as if they were on a local network, often 
for security reasons.

## OSI Model

Historically, one method of talking about the different layers of network communication is the OSI model. OSI stands for Open Systems Interconnect.

This model defines seven separate layers. The layers in this model are:
- Application: The application layer is the layer that the users and user-applications most often interact with. Network communication is discussed in terms of availability of resources, partners to communicate with, and data synchronization.
- Presentation: The presentation layer is responsible for mapping resources and creating context. It is used to translate lower level networking data into data that applications expect to see.
- Session: The session layer is a connection handler. It creates, maintains, and destroys connections between nodes in a persistent way.
- Transport: The transport layer is responsible for handing the layers above it a reliable connection. In this context, reliable refers to the ability to verify that a piece of data was received intact at the other end of the connection.
- This layer can resend information that has been dropped or corrupted and can acknowledge the receipt of data to remote computers.
- Network: The network layer is used to route data between different nodes on the network. It uses addresses to be able to tell which computer to send information to. This layer can also break apart larger messages into smaller chunks to be reassembled on the opposite end.
- Data Link: This layer is implemented as a method of establishing and maintaining reliable links between different nodes or devices on a network using existing physical connections.
- Physical: The physical layer is responsible for handling the actual physical devices that are used to make a connection. This layer involves the bare software that manages physical connections as well as the hardware itself (like Ethernet).

As you can see, there are many different layers that can be discussed based on their proximity to bare hardware and the functionality that they provide.

TCP/IP Model

The TCP/IP model, more commonly known as the Internet protocol suite, is another layering model that is simpler and has been widely adopted. It defines the four separate layers, some of which overlap with the OSI model:

Application: In this model, the application layer is responsible for creating and transmitting user data between applications. The applications can be on remote systems, and should appear to operate as if locally to the end user.
The communication is said to take place between peers.

Transport: The transport layer is responsible for communication between processes. This level of networking utilizes ports to address different services. It can build up unreliable or reliable connections depending on the type of protocol used.

Internet: The internet layer is used to transport data from node to node in a network. This layer is aware of the endpoints of the connections, but does not worry about the actual connection needed to get from one place to another. IP addresses are defined in this layer as a way of reaching remote systems in an addressable manner.

Link: The link layer implements the actual topology of the local network that allows the internet layer to present an addressable interface. It establishes connections between neighboring nodes to send data.

As you can see, the TCP/IP model, is a bit more abstract and fluid. This made it easier to implement and allowed it to become the dominant way that networking layers are categorized.

Interfaces
Interfaces are networking communication points for your computer. Each interface is associated with a physical or virtual networking device.

Typically, your server will have one configurable network interface for each Ethernet or wireless internet card you have.

In addition, it will define a virtual network interface called the "loopback" or localhost interface. This is used as an interface to connect applications and processes on a single computer to other applications and processes. You can see this referenced as the "lo" interface in many tools.

Many times, administrators configure one interface to service traffic to the internet and another interface for a LAN or private network.

In DigitalOcean, in datacenters with private networking enabled, your VPS will have two networking interfaces (in addition to the local interface). The "eth0" interface will be configured to handle traffic from the internet, while the "eth1" interface will operate to communicate with the private network.

Protocols
Networking works by piggybacking a number of different protocols on top of each other. In this way, one piece of data can be transmitted using multiple protocols encapsulated within one another.

We will talk about some of the more common protocols that you may come across and attempt to explain the difference, as well as give context as to what part of the process they are involved with.

We will start with protocols implemented on the lower networking layers and work our way up to protocols with higher abstraction.

Media Access Control

Media access control is a communications protocol that is used to distinguish specific devices. Each device is supposed to get a unique MAC address during the manufacturing process that differentiates it from every other device on the internet.

Addressing hardware by the MAC address allows you to reference a device by a unique value even when the software on top may change the name for that specific device during operation.

Media access control is one of the only protocols from the link layer that you are likely to interact with on a regular basis.

IP

The IP protocol is one of the fundamental protocols that allow the internet to work. IP addresses are unique on each network and they allow machines to address each other across a network. It is implemented on the internet layer in the IP/TCP model.

Networks can be linked together, but traffic must be routed when crossing network boundaries. This protocol assumes an unreliable network and multiple paths to the same destination that it can dynamically change between.

There are a number of different implementations of the protocol. The most common implementation today is IPv4, although IPv6 is growing in popularity as an alternative due to the scarcity of IPv4 addresses available and improvements in the protocols capabilities.

ICMP

ICMP stands for internet control message protocol. It is used to send messages between devices to indicate the availability or error conditions. These packets are used in a variety of network diagnostic tools, such as ping and traceroute.

Usually ICMP packets are transmitted when a packet of a different kind meets some kind of a problem. Basically, they are used as a feedback mechanism for network communications.

TCP

TCP stands for transmission control protocol. It is implemented in the transport layer of the IP/TCP model and is used to establish reliable connections.

TCP is one of the protocols that encapsulates data into packets. It then transfers these to the remote end of the connection using the methods available on the lower layers. On the other end, it can check for errors, request certain pieces to be resent, and reassemble the information into one logical piece to send to the application layer.

The protocol builds up a connection prior to data transfer using a system called a three-way handshake. This is a way for the two ends of the communication to acknowledge the request and agree upon a method of ensuring data reliability.

After the data has been sent, the connection is torn down using a similar four-way handshake.

TCP is the protocol of choice for many of the most popular uses for the internet, including WWW, FTP, SSH, and email. It is safe to say that the internet we know today would not be here without TCP.

UDP

UDP stands for user datagram protocol. It is a popular companion protocol to TCP and is also implemented in the transport layer.

The fundamental difference between UDP and TCP is that UDP offers unreliable data transfer. It does not verify that data has been received on the other end of the connection. This might sound like a bad thing, and for many purposes, it is. However, it is also extremely important for some functions.

Because it is not required to wait for confirmation that the data was received and forced to resend data, UDP is much faster than TCP. It does not establish a connection with the remote host, it simply fires off the data to that host and doesn't care if it is accepted or not.

Because it is a simple transaction, it is useful for simple communications like querying for network resources. It also doesn't maintain a state, which makes it great for transmitting data from one machine to many real-time clients. This makes it ideal for VOIP, games, and other applications that cannot afford delays.

HTTP

HTTP stands for hypertext transfer protocol. It is a protocol defined in the application layer that forms the basis for communication on the web.

HTTP defines a number of functions that tell the remote system what you are requesting. For instance, GET, POST, and DELETE all interact with the requested data in a different way.

FTP

FTP stands for file transfer protocol. It is also in the application layer and provides a way of transferring complete files from one host to another.

It is inherently insecure, so it is not recommended for any externally facing network unless it is implemented as a public, download-only resource.

DNS

DNS stands for domain name system. It is an application layer protocol used to provide a human-friendly naming mechanism for internet resources. It is what ties a domain name to an IP address and allows you to access sites by name in your browser.

SSH

SSH stands for secure shell. It is an encrypted protocol implemented in the application layer that can be used to communicate with a remote server in a secure way. Many additional technologies are built around this protocol because of its end-to-end encryption and ubiquity.

There are many other protocols that we haven't covered that are equally important. However, this should give you a good overview of some of the fundamental technologies that make the internet and networking possible.

* http://www.thegeekstuff.com/2011/11/tcp-ip-fundamentals/
- [ ] [Khan Academy](https://www.khanacademy.org/computing/computer-science/internet-intro)
- [ ] [UDP and TCP: Comparison of Transport Protocols](https://www.youtube.com/watch?v=Vdc8TCESIg8)
- [ ] [TCP/IP and the OSI Model Explained!](https://www.youtube.com/watch?v=e5DEVa9eSN0)
- [ ] [Packet Transmission across the Internet. Networking & TCP/IP tutorial.](https://www.youtube.com/watch?v=nomyRJehhnM)
- [ ] [HTTP](https://www.youtube.com/watch?v=WGJrLqtX7As)
- [ ] [SSL and HTTPS](https://www.youtube.com/watch?v=S2iBR2ZlZf0)
- [ ] [SSL/TLS](https://www.youtube.com/watch?v=Rp3iZUvXWlM)
- [ ] [HTTP 2.0](https://www.youtube.com/watch?v=E9FxNzv1Tr8)
- [ ] [Video Series (21 videos)](https://www.youtube.com/playlist?list=PLEbnTDJUr_IegfoqO4iPnPYQui46QqT0j)
- [ ] [Subnetting Demystified - Part 5 CIDR Notation](https://www.youtube.com/watch?v=t5xYI0jzOf4)
- [ ] Sockets:
    - [ ] [Java - Sockets - Introduction (video)](https://www.youtube.com/watch?v=6G_W54zuadg&t=6s)
    - [ ] [Socket Programming (video)](https://www.youtube.com/watch?v=G75vN2mnJeQ)
- https://support.dnsimple.com/categories/dns/
