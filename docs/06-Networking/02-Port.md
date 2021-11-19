# Ports

  - In this section we will learn about networking ports

  #### Port (computer networking)
 
 A port in computer networking is a virtual point where network connections start and end. With the use of ports, a computer can use a single physical network connection to handle many incoming and outgoing requests by assigning a port number to each. The numbers go from 0 to 65535, which is a 16-bit number. 
 
 Some of these port numbers are specifically defined and always associated with a specific type of service -- for example, File Transfer Protocol (FTP) is always port number 21 and Hypertext Transfer Protocol web traffic is always port 80. As the result, ports allow computers to easily differentiate between different kinds of traffic: emails go to a different port than webpages, for instance, even though both reach a computer over the same Internet connection. 
 
 In general, port numbers lower than 1024 identify the historically most commonly used services and are called the well-known port numbers. Higher-numbered ports are available for general use by applications and are known as ephemeral ports.

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
 
A port is always associated with a protocol, such as Transmission Control Protocol(TCP) or User Datagram Protocol(UDP). The port is specified by having the URL or IP address followed by a colon then the port number -- as examples, 10.0.0.1:80 or https://issai.nu.edu.kz:443. With all internet communication, there is always an associated port, but it may not be shown to the user as it is often implied by the type of communication.

A computer can manage many simultaneous connections on a single inbound port. This is because the local IP address, local port, remote IP address and remote port specify each connection. A listening port is when the computer is actively waiting for inbound requests on that port number, allowing those connections. Port forwarding is when communication to one address on a specific port is then sent, or forwarded, to another computer for processing.

 
References:
1. https://www.techtarget.com/searchnetworking/definition/port
2. https://en.wikipedia.org/wiki/Port_(computer_networking)
3. https://www.cloudflare.com/en-ca/learning/network-layer/what-is-a-computer-port/
4. https://opensource.com/article/18/10/common-network-ports
