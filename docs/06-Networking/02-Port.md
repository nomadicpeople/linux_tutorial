# Ports

  - In this section we will learn about networking ports

  #### Port (computer networking)
 
  - In computer networking, a port is a communication endpoint. At the software level, within an operating system, a port is a logical construct that identifies a specific process or a type of network service. 
  - A port is identified for each transport protocol and address combination by a 16-bit unsigned number, known as the port number. The most common transport protocols that use port numbers are the Transmission Control Protocol (TCP) and the User Datagram Protocol (UDP).

 - A port number is always associated with an IP address of a host and the type of transport protocol used for communication. It completes the destination or origination network address of a message. Specific port numbers are reserved to identify specific services so that an arriving packet can be easily forwarded to a running application. For this purpose, port numbers lower than 1024 identify the historically most commonly used services and are called the well-known port numbers. Higher-numbered ports are available for general use by applications and are known as ephemeral ports.
- Ports provide a multiplexing service for multiple services or multiple communication sessions at one network address. In the client–server model of application architecture, multiple simultaneous communication sessions may be initiated for the same service.
Port number
- A port number is a 16-bit unsigned integer, thus ranging from 0 to 65535. For TCP, port number 0 is reserved and cannot be used, while for UDP, the source port is optional and a value of zero means no port. A process associates its input or output channels via an internet socket, which is a type of file descriptor, associated with a transport protocol, an IP address, and a port number. This is known as binding. A socket is used by a process to send and receive data via the network. The operating system's networking software has the task of transmitting outgoing data from all application ports onto the network, and forwarding arriving network packets to processes by matching the packet's IP address and port number to a socket. For TCP, only one process may bind to a specific IP address and port combination. Common application failures, sometimes called port conflicts, occur when multiple programs attempt to use the same port number on the same IP address with the same protocol.
 
 
 
 #### Common port number
 ![port](https://user-images.githubusercontent.com/73333051/141141782-49c8c3f4-7fda-423f-bdd0-5baad4d5d717.png)




