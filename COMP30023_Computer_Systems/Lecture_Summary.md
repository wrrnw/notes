# COMP30023 Computer Systems Lecture Summary
## Lecture 1
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
## Lecture 2
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
- The layer Application, Transport, Network are end to end
- The layer Link, Physical are point to point
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
	- HTTP Response Message Format
		![HTTP Response Format](Image/HTTP_Response.png)
