# COMP30023 Computer Systems Lecture Summary
## Week 1 Lecture 1
- **What is Internet?**
	- Internet is a network that interconnects with hundreds of millions of computing devices
	- These devices are called *end systems* or *hosts*
- **Connection: End Systems - Routers - Modems - ISP**
	- ISP: Internet Services Providers(Telstra, TPG, etc.)
	- Packets: Information sent through the communication links
- **Protocols: defines the format and order of messages exchanged between different communicating entities, as well as the action taken on the transmission or receipt of a message or other events**
	- All activities in the internet involves two or more communicating remote entities is governed by protocols
	-  The communication between different entities requires different protocols
- **Layering model:**
	- Each layer offers services to the layer directly above it by:
		- Performing certain actions within the layer
		- Using the services by the layer directly below it
	- Strength:
		- An abstract way to represent the whole system
		- People at a layer
			- Only focus on the services provided to the upper layer
			- Only need to know the API's of the lower layer
			- Do not need to know the implementation details of all other layers
	- Drawbacks:
		- Introduce overheads
		- Inefficient and has delays
		- Increase the chance to make errors
- **Service Models:**
	- TCP/IP Model: Application Layer - Transport Layer - Network Layer - Link Layer - Physical Layer
	- OSI Model(Open Systems Interconnection): Application Layer - Presentation Layer - Session Layer - Transport Layer - Network Layer - Link Layer - Physical Layer


## Week 1 Lecture 2
- **Overview of TCP/IP Model**
	- **Application Layer**
		- The packets of information at this layer are called *messages*
		- It includes network applications and their application-layer protocols
		- Main protocols:
			- HTTP(HyperText Transfer Protocol): Web
			- FTP(File Transfer Protocol): File Transfer between end systems
			- SMTP(Simple Mail Transfer Protocol): email
			- DNS(Domain Name Systems): network-name to network-address translation
		- The application in one end system uses the protocol to exchange packets of information with the application in another end system
	- **Transport Layer**
		- The packets of information at this layer are called *segment*
		- It transports application-layer message between application endpoints
		- Main protocols:
			- TCP(Transmission Control Protocol):
				- Connection-Oriented Services
				- Reliable
			- UDP(User Datagram Protocol):
				- Connectionless Services
				- Unreliable
	- **Network Layer**
		- The packets of information at this layer are called *datagram*
		- It is responsible for moving network-layer packets from one end system to another end system
		- Main protocols:
			- IP(Internet Protocol)
				- It defines the fields in packets
				- It defines how the end systems and routers act on these fields
				- All Internet components have Internet layer *must run the IP protocol*
			-  Routing Protocol
				- It *determines the routes* the packets take between source and destination
				- The network layer routes a packet through a series of routers between the source and the destination
				- To move the packet from one node to the next node in the route, the network layer needs to *pass the datagram down* to the link layer
	- **Link Layer**
		- The packets of information at this layer are called *frame*
		- It delivers the packets to the next nodes along the route
		- The delivery services depends on specific link-layer protocol that is employed over the link, which means they are *link dependent*
	- **Physical Layer**
		- While the job of the link layer is to move the entire frame from one network element to the next element in the route, the job of the physical layer is to move the individual bits within the frames from the network element to the next
		- The protocols at this layer are also link dependent and further depend on the actual transmission medium of the link
- The Application layer, Transport layer, Network layer are end to end
- The Link layer, Physical layer are point to point
- **Overview of the OSI(Open Systems interconnection) model**
	- Except for layer 5, 6, all other layers have roughly the same functionalities as TCP/IP model
	- **Presentation Layer**
		- To provide services that allow communicating application to *interpret the meaning of the data exchanged*
		- The service includes data compression, data encryption, data description
		- It allows the application not to worry about the internal format in which data are represented and stored
	- **Session Layer**
		- It provides for delimiting and synchronization of data exchange, including the means to build a checkpointing and recovery scheme
- **Application Layer in depth**
	- Sockets
		- The interface between the application layer and the transport layer
		- Applications send and receive message through sockets
		- Each socket has a *unique identifier*
		- The format of the identifier depends on what transport-layer protocol is used(whether UDP or TCP)
		- Each transport-layer segment has a set of fields for identifying sockets
	- HTTP
		- The HTTP needs to be implemented in two programs: client program and server program
		- The client program and the server program are executing on the different end systems and talk to each other by exchanging HTTP messages
		- *Web page*: a document consisting of objects
		- *Object*: a file that is addressable by URL, such as a HTML file, a JPEG image, a JAVA applet, and a video clip
		- *URL(Uniform Resource Locator)*: consists of
			1. the *hostname* of the server that houses the objects
			2. the objects *path name*
			![URL Example](Image/URL_example.png)
		- Web browsers implement the client side of HTTP while the web servers implement the server side of HTTP
		- Most web pages include a base html file and several referenced objects
- **Two types of connections**
	- Non-persistent connection: Each request and response pair is sent over a separate TCP connection
		- For each objects, it requires **two** "round trip time"(One to *initiates the TCP connection* and one for *HTTP request*) plus the *file transmission time*
		- For each TCP connection, it causes OS *overhead* because TCP buffers must be allocated and the TCP variables must be kept in both client and server
		- Browsers often open *parallel* TCP connections to fetch referenced objects  
	- Persistent connection: All the requests and responses are sent over the same TCP connection
		- The default option for HTTP
		- Server leaves connection open after sending response. The connection closes if it is not used for certain amount of time(configurable)
		- Subsequent HTTP messages between the same client server are sent over the open connection
		- client can send request as soon as it encounters a referenced object, without waiting for replies to pending requests(pipelining)
- **How Non-persistent connection works when open the url http://www.someuni.edu.au/somedepartment/home.index**
	1. The HTTP client initiates a TCP connection(via its socket) to the server www.someuni.edu.au on port *80*(the default port number for HTTP)
	2. The HTTP server process accepts the connection requests and send a *response message*(via its socket)
	3. The HTTP client process sends a HTTP *request message*(via its socket) to the HTTP server. The request message includes the path name /somedepartment/home.index
	4. The HTTP server process:
		1. receives the request message(via its socket)
		2. retrieves the objects at the path name /somedepartment/home.index
		3. encapsulate the object in an HTTP *response message*
		4. send it to the client(via its socket)
	5. The HTTP server process tells the TCP to close the TCP connection. But the TCP does not actually terminate the connection until it knows for sure the client has received the response message intact
	6. The HTTP client receives the response message(via its socket). The TCP connection terminates. The message indicates that the encapsulated objects is an HTML file. The client:
		1. Extracts the HTML file from the message
		2. Examine the HTML file
		3. Find reference to all other objects
	7. The first four steps are then repeated for each of the referenced objects
- **HTTP Message**
	- HTTP Request Message Format
		![HTTP Request Format](Image/HTTP_Request.png)
		- Request line: method | URL | Version
		- Request methods:
			- GET: Request an object in the specific URL
			- POST: It is used when the user fills out the form
			- HEAD: Detect whether an object can be requested successfully
			- PUT: It allows a user to upload an object to a specific path on a specific Web server
			- DELETE: It allows a user to delete an object on a Web server
	- HTTP Response Message Format
		![HTTP Response Format](Image/HTTP_Response.png)
		- Status line: version | status code | phrase
		- HTTP response code:
			- 1xx: Information
				- 100 - Server agrees to handle client's request
			- 2xx: Success
				- 200 - Request succeeded
				- 204 - No content present
			- 3xx: Redirection
				- 301 - Page moved
				- 304 - Cached page still valid
			- 4xx: Client error
				- 403 - Forbidden page
				- 404 - Page not found
			- 5xx: Server error
				- 500 - Internal server error
				- 503 - Try again later
- **Cookie**
	- Background: HTTP is a *stateless* protocol. An HTTP server maintains no information about the clients. For allowing Web servers to identify users, HTTP uses *cookies*
	- The cookie has four components:
		1. A *cookie header line* in HTTP response message
		2. A *cookie header line* in HTTP request message
		3. A *cookie file* kept on user's end system and managed by the user's browser
		4. A back-end *database* at the Web site
![Cookie Example](Image/Cookie_example.png)


## Week 2 Lecture 1
- **File Transfer Protocol(FTP)**
	- In a typical FTP session, the user is *local host* and wants to transfer files to and from a *remote host*
	- FTP uses two parallel TCP connections to transfer a file:
		- Control connection:
			-  Sending control information between the two hosts including:
				- User identification, Password, Commands to change remote directory, Commands to "put" and "get" files
			- At the beginning, the client side initiates a TCP control connection to the server on port 21
			- The client side sends the user identification, password as well as the commands over this control connection during the entire FTP session(Persistent)
			- The commands and replies are sent over the control connection in 7-bit ASCII format.
			- Each command consists of four uppercase ASCII characters, some with optional arguments. Some common commands:
				- USER *username*: Used to send the user identification to the server
				- PASS *password*: Used to send user password to the server
				- LIST: Used to send back a list of all the files in the current remote directory. The list of files is sent over a *new and non-persistent data connection*
				- RETR *filename*: Used to retrieve (i.e., get) a file from the current directory of the remote host
				- STOR *filename*: Used to store (i.e., put) a file into the current directory of the remote host
			- The replies are *three-digit number*, followed by an optional message. Some typical replies:
				- 331 Username OK, password required
				- 125 Data connection already open; transfer starting
				- 425 Can't open data connection
				- 452 Error writing file
		- Data connection:
			- Automatically send a file
			- When the server side receives a command for a file transfer(either to or from the remote host), the server side initiates a TCP data connection to the client side at port 20
			- FTP sends exactly one file over the data connection after which the data connection *will be closed*(Non-persistent)
- **Simple Mail Transfer Protocol(SMTP)**
	- Three major components in email systems:
		- User agents
		- Mail servers
		- Simple Mail Transfer Protocol(SMTP)
	- SMTP: Transfer messages from the *senders' mail servers* to the *recipients' mail servers*
	- Mail message format
![Mail message format](Image/Mail_msg_format.png)
	- An overview example of SMTP
		1. Alice composes a message with Bob's email address
		2. Alice's user agent sends the message to her mail server
		3. The client side of SMTP on Alice's mail server opens a *direct persistent TCP connection* to an SMTP server at *port 25* on Bob's mail server
		4. The client side sends the message over the TCP connection
		5. The SMTP server side receives the messages and place it into Bob's mailbox
		6. Bob invokes his user agent to obtain the message at his convenience
	- Comparison between HTTP and SMTP
		- Similarity
			- Both of HTTP and SMTP are used to transfer files from one host to another
			- Both HTTP and SMTP use persistent TCP connection
		- Difference
			- HTTP is mainly a pull protocol. SMTP is primarily a push protocol
			- SMTP requires each message, including the body of the each message to be in *7-bit ASCII format*. HTTP does not has this restriction
			- HTTP encapsulates each object in its own HTTP response message. SMTP places all of message's objects into one message
	- Mail Access Protocol
		- Bob cannot use SMTP to obtain the message. Because SMTP is a push protocol, while obtaining messages is a pull operation
		- To obtain message from mail server, we use Mail Access Protocol:
			- Post Office Protocol - Version 3 (POP3)
			- Internet Mail Access Protocol (IMAP)
			- HTTP
- **Domain Name System(DNS)**
	- An application-layer protocol to *translate user-defined host name to IP address*
	- The DNS adds an additional delay to the Internet Applications that uses it
	- All DNS query and reply messages are sent through UDP datagrams to port 53
	- In addition to translate hostnames to IP addresses, DNS also provides services:
		- Host aliasing
			- A host can have one or more alias names
		- Mail Server aliasing
		- Load distribution
	- Distributed, Hierarchical database of mappings
		- Problems with centralized database
			- A single point of failure
			- Traffic volume
			- Distant centralized database
			- Maintenance
		- DNS uses a large number of servers, organized hierarchical and distributed around world. No single DNS server has all of the mappings for all of the hosts in the Internet. Mappings are distributed around the DNS servers
![Hierarchy of DNS Server](Image/Hierarchy_of_DNS_server.png)
		- Root DNS Servers:
			- 13 root DNS servers over the world
		- Top-Level Domain(TLD) DNS Servers:
			- Top-level domain such as *com*, *org*, *net*, *edu* and *gov*
			- All of the country top-level domains such as *au*, *uk*, *fr*, *ca* and *jp*
		- Authoritative DNS Server
			- Every organization with publicly accessible on the internet *must* provide publicly accessible DNS records that maps the name of those hosts to IP addresses
			- An organization DNS server houses these DNS records
		- Local DNS Server
			- Each ISP, such as an university, an company or a residential ISP has a local DNS server (also called a default name server)
			- When a host makes a DNS query, the query is sent to the local DNS server, which acts like a proxy, forwarding the query into the DNS server hierarchy



## Week 2 Lecture 2 - Git
- **Version Control**
	- Version control is a system that records the changes to a file or set of files over time so that we can recall specific version later
	- Local Version Control System
		- Duplicate files in different directories
	- Centralized Version Control Systems(CVCS)
		- A single server contains all the version files, and a number of clients that check out files from that central place
			- CVS
			- SVN
			- Perforce
	- Distributed Version Control Systems(DVCS)
		- Clients don't just check out the latest snapshot of the files; rather, they fully mirror the repository, including the its full history
			- Git
			- Mercurial
			- Bazaar
			- Darcs
	- Why do we use Git?
		- While those other version control system utilize delta-based version control, Git uses a series of snapshot
		- Uses checksums
			- Everything in Git is checksummed before it is stored and is then referred to by checksum
			- The checksum is a 40-character string composed of hexadecimal characters(0-9 and a-f), which is computed by SHA-1 hash based on the content of a file and the directory structure in Git. For example, 24b9da6552252987aa493b52f8696cd6d3b00373
		- Nearly all operations is Local
			- Most of operation in Git need only local files and resources to operate. Because Git stores the entire history of the project in each local computer
	- Three Stages in Git
		- Modified
			- The file has changed but not yet been committed to the database
		- Staged
			- The current version of the modified file is marked to be put into the next commit snapshot
		- Committed
			- The file is safely stored in local database
![Git](Image/Git.png)
	- Branching Feature



## Week 3 Lecture 1
- **Transport-Layer Services**
	- An application protocol passes the message to the transport layer via sockets
	- A transport-layer protocol provides for logic communication between application processes running on different hosts
	- The transport layer passes the segment to the network layer at the sending end system
- **The relation between Transport Layer and Network Layer**
	- A transport-layer protocol provides for *logic communication between application processes running on different hosts*
	- A network-layer protocol provides *logical communication between different hosts*
	- So, a transport-layer protocol is *process-to-process*, while a network-layer protocol is *host-to-host*
![Transport Layer and Network Layer](Image/Transport_layer.png)
	- An analogy in reality
![Transport Layer and Network Layer Analogy](Image/Analogy.png)
- **Service from the Network Layer**
	- It has IP(Internet Protocol)
		- IP provides logical communication between hosts
		- IP is an unreliable service:
			- It does not guarantee *segment delivery*
			- It does not guarantee *orderly delivery* of segments
			- It does not guarantee the *integrity of the data* in the segments
- **Multiplexing and Demultiplexing**
	- In order to extend the host-to-host delivery service to process-to-process delivery service
	- The transport layer at receiving host does not actually deliver the data directly to a process, but instead to an intermediary socket
	- Demultiplexing
		- At the receiving end, the transport layer examines the fields in segment to *identify* the receiving sockets and then *direct* the segment to that socket
	- Multiplexing
		- *Gather* data chunks at the source host from different sockets
		- *Encapsulate* each data chunk with header information to create segments
		- *Pass* the segments to the network layer
- **User Datagram Protocol(UDP)**
	- no-frills and bare-bone
	- It does as little as a transport-layer can do
		- Multiplexing and Demultiplexing
			- In UDP, sockets are *identified by port numbers*
		- Some light error checking
	- Except for above two jobs, it adds nothing to IP
	- *Connectionless* and *unreliable*
		- No guarantee on *delivery*, *order* and *integrity*
	![UDP Segment Structure](Image/UDP_segment_structure.png)
- **Why do we still need UDP?**
	- Finer application-level control over what is sent and when
		- Data is sent immediately
		- No congestion control
		- Real-time applications often:
			- require minimum sending rate
			- do not want to overly delay segment transmission
			- can tolerate some data loss
	- No connection establishment
		- A principle reason why DNS runs over UDP rather than TCP
	- No connection state
		- Low system overhead(no buffers, no parameters)
	- Small packet header overhead
		- UDP has only 8 bytes of overhead, while TCP has 20
- **UDP Checksum**
	- The UDP checksum is used to determine whether bits within the UDP segment have been altered as it moves from source to destination
	- The UDP checksum at the sender side is computed as follows:
		- Compute the sum of all the 16-bit words in the segment, with overflow encountered during the sum being wrapped around
		- Compute the 1s complement of the sum
		- The result is put in the checksum field of the UDP segment
	- Example
	![UDP checksum example 1](Image/UDP_checksum_example1.png)
	![UDP checksum example 2](Image/UDP_checksum_example2.png)
	![UDP checksum example 3](Image/UDP_checksum_example3.png)
	- Error Detection by UDP Checksum
		- At the receiver, compute the sum of all 16-bit words and the checksum
			- If no errors are introduced into the packet, then clearly the sum at the receiver will be 1111111111111111
				- Even though we get 1111111111111111, it still not guarantee that there is no error in the segment(If the same digit of two words corrupted, the result remains the same). Nonetheless, if we know that the corruption is just on one bit, then checksum can guarantee to correctly detect the corruption
			- Otherwise, we know that there must be some errors in the packet


# Week 3 Lecture 2 - RDT
- **Over a Perfectly Reliable Channel: rdt 1.0**
	![rdt1.0 picture1](Image/rdt1.0_pic1.png)
	![rdt1.0 picture2](Image/rdt1.0_pic2.png)
- **Over a Channel with Bit Errors: rdt 2.0**
	- bits in a packet may be corrupted
	- The positive and negative acknowledgements allow the receiver to let the sender know what has been received correctly, what has been received in error and thus requires repeating
	- Reliable data transfer protocols based on such retransmission are known as ARQ(Automatic Repeat reQuest) protocols
	- Three additional protocol capabilities are required in ARQ protocols
		- Error detection
			- A mechanism (e.g. checksum) to allow receiver to detect bit errors
		- Receiver feedback
			- Explicit positive (ACK) and negative (NAK) acknowledgements (i.e., packets) from the receiver to the sender
			- One bit suffices, i.e., 1 = ACK and 0 = NAK
		- Retransmission
			- The sender needs to retransmit a packet when it is received in errors at the receiver
		![rdt2.0 picture1](Image/rdt2.0_pic1.png)
		![rdt2.0 picture2](Image/rdt2.0_pic2.png)
- **Over a Channel with Bit Errors: rdt 2.1**
	- Since the ACK/NAK could also corrupt. The question is how the protocol should handle the errors in ACK/NAK
		- The sender resends the current data packet when it receives the garbled ACK or NAK packet
			- Issue: The receiver cannot know the a priori whether the arriving packet contains new data or is a retransmission
			- Solution: Add a new field called sequence number in the data packet. In a stop-and-wait protocol, a 1-bit sequence number will suffice. Specifically, the sender alternates the 1-bit sequence number between 0 and 1 for every new data packet
		![rdt2.1 picture1](Image/rdt2.1_pic1.png)
		![rdt2.1 picture2](Image/rdt2.1_pic2.png)
- **Over a Channel with Bit Errors: rdt 2.2**
	- Get rid of NAK packets from rdt 2.1
	- Instead of sending a NAK packet to the sender, the receiver sends an ACK packet for the last correctly received packet
	- For example, the last correctly received packet at receiver has sequence number 1. If the receiver now gets a corrupted packet:
		- In rdt 2.1, it needs to send a NAK packet
		- In rdt 2.2, it sends an ACK packet indicating that the last correctly received packet is with sequence number 1. In this case, the sender knows that the receiver doesn't receive the packet with sequence number 0, and thus, resend the packet.
		![rdt2.2 picture1](Image/rdt2.2_pic1.png)
		![rdt2.2 picture2](Image/rdt2.2_pic2.png)
- **Over a Lossy Channel with Bit Errors: rdt 3.0**
	- In addition to corrupted bits, the underlying channel can also lose packets
	- Two additional protocol capabilities must be addressed
		- Detect packet loss
			- Timer can help
		- Retransmission when packet loss
			- The techniques of checksums, sequence numbers, ACK packets and retransmissions developed in rdt 2.2 are sufficient to solve
		![rdt3.0 picture1](Image/rdt3.0_pic1.png)
		![rdt3.0 picture2](Image/rdt3.0_pic2.png)
		![rdt3.0 picture3](Image/rdt3.0_pic3.png)


# Week 4 Lecture 1
- **Pipelined RDT Protocols**
	- Although rdt3.0 is functionally correct, the performance is not satisfied because it is a stop-and-wait protocol
	- The sender is allowed to send multiple packets without waiting for acknowledgement through pipelined rdt protocol
	- Problem:
		- The 1-bit sequence number is no longer sufficient. Each packet in-transit must have a unique sequence number
		- Buffers in both the sender and the receiver are needed
			- The sender may need to buffer the packets that have been transmitted but not yet acknowledged
			- The receiver may need to buffer the packets that have been correctly received
- **Transmission Control Protocol(TCP)**
	- TCP is a type of Pipelined RDT
	- TCP is *connection-oriented*, because two processes must "handshake" before sending data
	- TCP creates a number of *variables* and *buffers* during the 3-way handshake
	![Three-way handshake](Image/three_way_handshake.png)
	- TCP is *full-duplex* such that both the two sides can send data to each other
	- TCP Structures
	![TCP Structure](Image/tcp_structure.png)
		- Sequence Number: The byte-stream number of the first byte in the data field of the segment
		- Acknowledgement Number: The acknowledgement number that Host A puts in its segment is the sequence number of the next byte that Host A is expecting from Host B
	- TCP only acknowledge bytes up to the first missing byte in the stream. Thus, TCP is said to provide *cumulative acknowledgements*
	- When receiver receives the out-of-order segments, it keeps the out-of-order segments and waits for the missing bytes to fill the gap
	![Telnet example](Image/telnet_example.png)

# Week 4 Lecture 2


# Week 5 Lecture 1


# Week 5 Lecture 2


# Week 6 Lecture 1 First Half Revision


# Week 6 Lecture 2 Mid-Sem Test


# Week 7 Lecture 1


# Week 7 Lecture 2


# Week 8 Lecture 1


# Week 8 Lecture 2


# Week 9 Lecture 1


# Week 10 Lecture 1


# Week 10 Lecture 2


# Week 11 Lecture 1


# Week 11 Lecture 2


# Week 12 Lecture 1
