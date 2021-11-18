# Ports

  - In this section we will learn about networking ports

  #### Port (computer networking)
 
 A port in computer networking is a virtual point where network connections start and end. With the use of ports, a computer can use a single physical network connection to handle many incoming and outgoing requests by assigning a port number to each. The numbers go from 0 to 65535, which is a 16-bit number. 
 
 Some of these port numbers are specifically defined and always associated with a specific type of service -- for example, File Transfer Protocol (FTP) is always port number 21 and Hypertext Transfer Protocol web traffic is always port 80. As the result, ports allow computers to easily differentiate between different kinds of traffic: emails go to a different port than webpages, for instance, even though both reach a computer over the same Internet connection.
 
#### Notable welll-known numbers
Number  | Assignment
------------- | -------------
20  | File Transfer Protocol (FTP) Data Transfer
21  | File Transfer Protocol (FTP) Command Control
22  | Secure Shell (SSH) Secure Login
23  | Telnet remote login service, unencrypted text messages 
25  | Simple Mail Transfer Protocol (SMTP) email delivery
53  | Domain Name System (DNS) service
67,68 | Dynamic Host Configuration Protocol (DHCP)
80  | Hyptertext Transfer Protocol (HTTP) used in the World Wide Web
110 | Post Office Protocol (POP3)
119 | Network News Transfer Protocol (NNTP)
123  | Network Time Protocl (NTP)
143  | Internet Message Access Protocol (IMAP) Management of digital mail
194  | INternet Relay Chat (ICR)
443  | HTTP Secure (HTTPS) HTTP over TLS/SSL
 
  A port number is always associated with an IP address of a host **clarify what a host means** and the type of transport protocol used for communication. It completes the destination or origination network address of a message. Specific port numbers are reserved to identify specific services so that an arriving packet can be easily forwarded to a running application. For this purpose, port numbers lower than 1024 identify the historically most commonly used services and are called the well-known port numbers. Higher-numbered ports are available for general use by applications and are known as ephemeral ports.

 Ports provide a multiplexing **what does this word mean?** service for multiple services or multiple communication sessions at one network address. In the client–server model of application architecture, multiple simultaneous communication sessions may be initiated for the same service.

<>A port number is a 16-bit unsigned integer, thus ranging from 0 to 65535. For TCP, port number 0 is reserved and cannot be used, while for UDP, the source port is optional and a value of zero means no port. A process associates its input or output channels via an internet socket, which is a type of file descriptor, associated with a transport protocol, an IP address, and a port number. This is known as binding. 

A socket is used by a process to send and receive data via the network. The operating system's networking software has the task of transmitting outgoing data from all application ports onto the network, and forwarding arriving network packets to processes by matching the packet's IP address and port number to a socket. For TCP, only one process may bind to a specific IP address and port combination. Common application failures, sometimes called port conflicts, occur when multiple programs attempt to use the same port number on the same IP address with the same protocol.
 
Citations:
1. https://www.techtarget.com/searchnetworking/definition/port
2. https://en.wikipedia.org/wiki/Port_(computer_networking)
