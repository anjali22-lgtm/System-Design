NETWOKRING
Networking is the backbone of any distributed system.  
It ensures that *data moves efficiently, reliably, and securely** between servers, clients, and other components.  

When you send a message on WhatsApp, stream a video, or deploy an API, countless networking layers work behind the scenes to make that communication reliable.
Data doesn't magically jump from one computer to another; it undergoes a meticulous journey, transformed and routed at each step.

1.OSI MODELS(Open system interconnection models)
The OSI model divides the process of network communication into seven distinct layers, each with specific responsibilities.
Think of it like a factory assembly line, where each station performs a specialized task before passing the product to the next.


A crucial concept is encapsulation: As data moves down the stack at the sender, each layer adds its own "header" (and sometimes a trailer) containing control information. 
When data moves up the stack at the receiver, each layer strips off its corresponding header.

-layer 1: (Physical layer)
The Physical Layer is responsible for the actual transmission of raw bits (0s and 1s) over the physical communication medium. 
It defines the electrical, mechanical, procedural, and functional specifications for activating, maintaining, and deactivating physical links.

Examples: Ethernet cables (Cat 5e, Cat 6), fiber optics, Wi-Fi radio frequencies, DSL, modems, hubs, repeaters.

-layer 2: (Data Link Layer)
The Data Link Layer ensures reliable transmission of data between directly connected nodes (i.e., devices on the same local network segment). It handles framing (dividing data into manageable units), physical addressing (using MAC addresses), and error detection/correction for the local link.

Examples: Ethernet, Wi-Fi (802.11 standards), ARP (Address Resolution Protocol), switches.

-layer 3:(Network layer)
The Network Layer is responsible for logical addressing (IP addresses) and routing data packets across potentially multiple interconnected networks. It determines the best path for data to travel from source to destination.

Protocols: IP (Internet Protocol), ICMP (Internet Control Message Protocol), OSPF (Open Shortest Path First), BGP (Border Gateway Protocol), routers.

-layer 4:(Transport layer)
The Transport Layer provides end-to-end communication between processes (applications) on different hosts. It handles segmentation of data, multiplexing (sending data from multiple applications over one network connection), and often reliable data transfer.

Protocols: TCP (Transmission Control Protocol) and UDP (User Datagram Protocol).

-layer 5:(Session layer)
The Session Layer is responsible for establishing, managing, and terminating communication sessions between applications. It handles things like authentication, authorization, and keeping track of which application sent which data.

Examples: While less distinct in modern TCP/IP implementations, concepts like RPC (Remote Procedure Call) sessions or WebSocket connections align with this layer's purpose.

-layer 6:(Presentation layer)
The Presentation Layer ensures that data is in a usable format for the Application Layer. It handles data translation, encryption/decryption, compression/decompression, and serialization/deserialization.

Examples: SSL/TLS (encryption), JSON, XML, Protocol Buffers (serialization), MIME (data format specification).

-layer 7:(Application layer)
The Application Layer is the closest to the end-user. It defines how applications interact with the network and provides user-facing services. This is where your actual software logic often resides.

Examples: HTTP, HTTPS, DNS, SMTP, FTP, SSH, Telnet, gRPC, WebSocket.


 Encapsulation and Decapsulation in Action
Let's trace a simple HTTP GET request from your browser to a web server:

Application Layer (L7): Your browser creates an HTTP GET request (GET /index.html HTTP/1.1).
Presentation Layer (L6): The data is prepared, possibly compressed, and then encrypted by TLS. The raw HTTP request becomes encrypted data.
Session Layer (L5): A TLS session is managed.
Transport Layer (L4): The encrypted data is segmented (if too large) and a TCP header is added, including source and destination port numbers (e.g., SRC=50000, DEST=443). This unit is now a TCP segment.
Network Layer (L3): An IP header is added, containing the source IP address of your computer and the destination IP address of the web server. This unit is now an IP packet.
Data Link Layer (L2): An Ethernet header and trailer are added, containing the source MAC address of your network card and the destination MAC address of your router (for the first hop). This unit is now an Ethernet frame.
Physical Layer (L1): The frame is converted into raw electrical signals or light pulses and sent over the physical medium (e.g., Wi-Fi radio waves, Ethernet cable).
At the web server, the process reverses:

Physical Layer (L1): Electrical signals are received and converted back into an Ethernet frame.
Data Link Layer (L2): The Ethernet header/trailer is removed, MAC addresses are checked. The IP packet is extracted.
Network Layer (L3): The IP header is removed, and the destination IP is checked. The TCP segment is extracted.
Transport Layer (L4): The TCP header is removed, destination port (443) is checked, and segments are reassembled. The encrypted data is passed up.
Session Layer (L5): The TLS session is managed.
Presentation Layer (L6): The data is decrypted by TLS and decompressed.
Application Layer (L7): The original HTTP GET request is delivered to the web server application, which then processes it.




IP ADDRESSES
Every time you visit a website, send an email, or make an API call, your device uses an IP address to identify itself.
This address ensures that the data you request finds its way back to you, and the data you send reaches its intended destination.

What do u mean by IP Address?
An IP address is a unique numerical label assigned to each device connected to a network that uses the Internet Protocol for communication. 
Think of it as a phone number for your computer or a mailing address for your laptop.
It serves two primary functions:

Identification: It uniquely identifies a device (or more accurately, a network interface) on the network. This tells other devices who is sending or receiving information.
Location Addressing: It specifies the location of the device in the network, providing a path for data to be delivered.

 IP Address Structure
An IP address isn't just a random number; it has a clear structure that is split into two main parts:

Network ID: This part of the address identifies the specific network the device is on. All devices on the same local network share the same Network ID.
Host ID: This part of the address identifies a specific device (like a computer, server, or smartphone) within that network.
For example, in the common IPv4 address 192.168.1.10 with a standard subnet mask, the breakdown is:

Network ID: 192.168.1
Host ID: 10
Routers primarily look at the Network ID. They don't need to know about every single device in the world, only which network a packet is destined for.
They use this information to forward the packet to the next router closer to the destination network.


## IPv4 vs IPv6

IP addressing is a fundamental part of networking, allowing devices to communicate over a network.  

| Feature              | IPv4                           | IPv6                                      |
|---------------------|--------------------------------|-------------------------------------------|
| Address Length       | 32 bits                        | 128 bits                                  |
| Address Format       | Decimal (e.g., 192.168.1.1)  | Hexadecimal (e.g., 2001:0db8::1)         |
| Number of Addresses  | ~4.3 billion                   | 3.4×10^38 (virtually unlimited)          |
| Header Complexity    | Simple                         | More complex, includes extension headers |
| Configuration        | Manual or DHCP                 | Auto-configuration supported             |
| Security             | Optional (IPSec)               | Built-in IPSec support                    |
| NAT Needed           | Often                          | Not required                              |

**Key Points:**
- **IPv4** is still widely used but running out of addresses.  
- **IPv6** solves address exhaustion and offers better security and auto-configuration.  
- Modern systems support both via **dual stack networks**.


## Public IP vs Private IP

IP addresses are used to identify devices on a network. They can be **public** or **private** depending on their scope.

| Feature               | Public IP Address                     | Private IP Address                        |
|-----------------------|-------------------------------------|------------------------------------------|
| Scope                 | Accessible over the Internet         | Accessible only within a private network |
| Uniqueness            | Globally unique                      | Unique only within the local network     |
| Example Range         | 8.8.8.8, 172.217.0.0               | 192.168.0.0 – 192.168.255.255, 10.0.0.0 – 10.255.255.255 |
| Assignment            | Provided by ISP (Internet Service Provider) | Configured by router or manually       |
| Use Case              | Connecting to the Internet           | Devices inside LAN (home/office network) |

**Key Points:**
- Public IP allows devices to communicate over the **Internet**.  
- Private IP is used for **internal communication** inside a network.  
- NAT (Network Address Translation) often maps private IPs to public IPs for Internet access.




DNS(DOMAIN NAME SYSTEM)
Imagine trying to remember the IP address of every website you want to visit—like having to memorize a phone number for every friend instead of just calling by name.
Thankfully, the Internet has a solution: the Domain Name System (DNS).

Think of DNS as the phone book of the Internet, translating easy-to-remember domain names (like www.example.com) into machine-friendly IP addresses (like 93.184.216.34).
The Domain Name System (DNS) is a distributed, hierarchical system designed to translate human-readable domain names into IP addresses, which are necessary for locating and communicating with servers on the Internet.

Instead of typing 93.184.216.34 into your browser, you simply enter , and DNS takes care of finding the corresponding IP address.

How DNS works?
The process of DNS resolution involves converting a hostname (such as www.example.com) into a computer-friendly IP address (such as 192.168.1.1). 
An IP address is given to each device on the Internet, and that address is necessary to find the appropriate Internet device - like a street address is used to find a particular home.
When a user wants to load a webpage, a translation must occur between what a user types into their web browser (example.com) and the machine-friendly address necessary to locate the example.com webpage.

In order to understand the process behind the DNS resolution, it’s important to learn about the different hardware components a DNS query must pass between.
For the web browser, the DNS lookup occurs "behind the scenes" and requires no interaction from the user’s computer apart from the initial request.

Hierarchical structure of DNS:

Conclusion
The Domain Name System (DNS) is an essential component of the Internet, acting as a distributed phone book that maps human-friendly domain names to machine-friendly IP addresses. 
Its hierarchical, distributed architecture ensures scalability, high availability, and resilience, even in the face of high query volumes or network failures.
From root servers to TLDs, authoritative name servers, and resolvers, each component of DNS plays a crucial role in ensuring that users can quickly and reliably access websites and online services.

With features like caching and security extensions such as DNSSEC, the DNS ecosystem is designed to meet the demanding needs of the modern Internet.



PROXY Vs REVERSE PROXY
Proxies and reverse proxies are servers that sit between clients and servers to improve security, privacy and performance.
A Proxy server (sometimes called a Forward proxy) acts on behalf of clients, while a Reverse Proxy acts on behalf of servers.

## Proxy Server

A **Proxy Server** acts as an intermediary between a client (user) and a server (destination).  
It receives requests from clients, forwards them to the destination server, and then returns the response back to the client.

### Key Functions:

1. **Anonymity & Security**
   - Hides the client's IP address from the destination server.
   - Helps protect internal networks from direct attacks.

2. **Content Filtering**
   - Can block access to certain websites or content.
   - Useful in corporate or educational environments.

3. **Caching**
   - Stores copies of frequently requested content.
   - Reduces latency and saves bandwidth.

4. **Load Balancing**
   - Distributes requests across multiple servers.
   - Improves availability and performance.

### Types of Proxy Servers:

- **Forward Proxy:** Sits between client and server; controls client access to external resources.  
- **Reverse Proxy:** Sits between server and client; controls access to the server and can distribute requests among multiple servers.


## Reverse Proxy Server

A **Reverse Proxy** sits **in front of one or more servers** and acts as an intermediary for requests coming from clients.  
Unlike a forward proxy (which serves the client), a reverse proxy **serves the server side**, managing incoming traffic and distributing it efficiently.

### Key Functions:

1. **Load Balancing**
   - Distributes incoming client requests across multiple backend servers.
   - Improves performance and ensures no single server is overloaded.

2. **Security & Anonymity**
   - Hides internal server IPs from clients.
   - Can provide SSL/TLS encryption, protection against attacks (like DDoS).

3. **Caching**
   - Stores frequently requested content to reduce backend load.
   - Speeds up response times for clients.

4. **Compression & Optimization**
   - Compresses responses for faster delivery.
   - Optimizes traffic between clients and servers.

### Example Use Case:
- Large websites like **Netflix, Amazon, or Google** use reverse proxies to handle millions of requests efficiently.



HTTP/HTTPS
Every time you interact with the internet, you're using HTTP (HyperText Transfer Protocol) or its secure counterpart, HTTPS.
These protocols are the fundamental language spoken between clients and servers, defining how information is requested and delivered.

HTTP:
## HTTP (Hypertext Transfer Protocol)

HTTP is the protocol that allows **communication between a client (browser, app) and a server** over the web.  

It works on a **request-response model**:  
1. The client sends an **HTTP request** to the server.  
2. The server processes the request and sends an **HTTP response** back to the client.  

### How HTTP Works:

1. **Client sends a request**  
   - Example: A browser requests `https://example.com/index.html`.
2. **Server processes the request**  
   - Finds the resource (HTML page, image, JSON data, etc.).
3. **Server sends response**  
   - Response contains the requested data and a **status code**.

---

### HTTP Methods (Verbs)

| Method | Purpose                                |
|--------|----------------------------------------|
| GET    | Retrieve data from the server           |
| POST   | Send new data to the server             |
| PUT    | Update existing data on the server      |
| PATCH  | Partially update data                   |
| DELETE | Remove data from the server             |
| HEAD   | Get headers only (no body)             |
| OPTIONS| Check supported HTTP methods on server |

---
### HTTP Status Codes

| Code | Meaning                       |
|------|-------------------------------|
| 200  | OK – Request succeeded        |
| 201  | Created – New resource created|
| 301  | Moved Permanently – Redirect  |
| 302  | Found – Temporary redirect    |
| 400  | Bad Request – Client error    |
| 401  | Unauthorized – Needs login   |
| 403  | Forbidden – Access denied     |
| 404  | Not Found – Resource missing  |
| 500  | Internal Server Error – Server problem |
| 503  | Service Unavailable           |

---


HTTPs
## HTTPS (Hypertext Transfer Protocol Secure)

HTTPS is the **secure version of HTTP**. It ensures that data sent between a client (browser/app) and server is **encrypted and protected** from eavesdropping or tampering.  
It works **exactly like HTTP**, but with an added layer of **SSL/TLS encryption**.

---

### How HTTPS Works:

1. **Client connects to the server**  
   - Browser requests a secure connection (e.g., `https://example.com`).
2. **Server sends SSL/TLS certificate**  
   - Verifies server identity and provides encryption keys.
3. **Secure session established**  
   - Data exchanged between client and server is encrypted.
4. **Client sends request**  
   - Just like HTTP (GET, POST, etc.), but encrypted.
5. **Server responds**  
   - Encrypted response sent back to the client.

---

### Key Features of HTTPS

| Feature               | Description                               |
|-----------------------|-------------------------------------------|
| Encryption            | Protects data from eavesdropping          |
| Authentication        | Ensures client talks to the correct server |
| Integrity             | Data cannot be tampered in transit        |
| Port                  | Default port is 443                        |

---

### HTTPS vs HTTP

| Aspect       | HTTP                  | HTTPS                        |
|-------------|----------------------|------------------------------|
| Security     | Not secure           | Secure (encrypted)           |
| Port        | 80                   | 443                          |
| Encryption  | None                 | SSL/TLS                       |
| URL Format  | http://example.com   | https://example.com          |

---

Differnce between Http and https?
## HTTP vs HTTPS

HTTP and HTTPS are protocols for transferring data between a client (browser/app) and a server.  
The main difference is **security**: HTTPS encrypts the data, while HTTP does not.

| Feature               | HTTP                                  | HTTPS                                   |
|-----------------------|--------------------------------------|----------------------------------------|
| Full Form             | Hypertext Transfer Protocol          | Hypertext Transfer Protocol Secure     |
| Security              | Not secure (data is sent in plain text) | Secure (data is encrypted using SSL/TLS) |
| Default Port          | 80                                   | 443                                     |
| URL Prefix            | http://                              | https://                                |
| Data Integrity        | No guarantee                         | Ensures data is not tampered            |
| Authentication        | None                                 | Server authentication using certificates |
| Use Case              | Non-sensitive data transfer          | Sensitive data (login, payments, personal info) |

---



TCP Vs UDP

## TCP vs UDP

TCP and UDP are two core **transport layer protocols** used for sending data over networks.  

### Comparison Table

| Feature             | TCP (Transmission Control Protocol)        | UDP (User Datagram Protocol)           |
|--------------------|-------------------------------------------|---------------------------------------|
| Connection Type     | Connection-oriented (establishes a connection before data transfer) | Connectionless (sends data without setup) |
| Reliability         | Reliable, ensures all packets are received in order | Unreliable, no guarantee of delivery or order |
| Error Checking      | Error detection and correction included   | Error detection only (optional)       |
| Data Flow Control   | Yes (controls flow to avoid congestion)  | No                                     |
| Speed               | Slower due to reliability overhead       | Faster, lightweight                   |
| Use Case Examples   | Web browsing (HTTP/HTTPS), Email (SMTP/IMAP), File transfer (FTP) | Video streaming, Online gaming, VoIP  |
| Packet Size         | Stream of bytes (segment)                 | Datagram (discrete messages)          |

---

### How TCP Works:
1. Establishes a **3-way handshake** before data transfer.  
2. Splits data into packets, sends them reliably.  
3. Ensures packets arrive **in order**.  
4. Retransmits lost packets automatically.  

### How UDP Works:
1. Sends data as **datagrams** without prior connection.  
2. No guarantee of order or delivery.  
3. Very fast and lightweight, ideal for **real-time applications**.  

---

✅ **Key Points:**
- **TCP** = reliable, ordered, connection-oriented (safe but slower).  
- **UDP** = fast, connectionless, no guarantee (lightweight, real-time apps).  



LOAD BALANCER
Load Balancer is a system that spreads incoming network traffic across multiple backend servers (often called “worker nodes” or “application servers”).
It ensures that no single server becomes a bottleneck due to an overload of requests. By distributing the load, applications can handle higher volumes of traffic and remain robust in the face of server failures.

Why Do We Need a Load Balancer?
Scalability: As traffic grows, you can add more servers behind the load balancer without redesigning your entire architecture.
High Availability: If one server goes offline or crashes, the load balancer automatically reroutes traffic to other healthy servers.
Performance Optimization: Balancing load prevents certain servers from overworking while others remain underutilized.
Maintainability: You can perform maintenance on individual servers without taking your entire application down.


Types of Load Balancers
Load balancers can be categorized in a few ways:

Hardware vs. Software
Hardware Load Balancer: Specialized physical devices often used in data centers (e.g., F5, Citrix ADC). They tend to be very powerful but can be expensive and less flexible.
Software Load Balancer: Runs on standard servers or virtual machines (e.g., Nginx, HAProxy, Envoy). These are often open-source or lower-cost solutions, highly configurable, and simpler to integrate with cloud providers.
Layer 4 vs. Layer 7
Layer 4 (Transport Layer): Distributes traffic based on network information like IP address and port. It doesn’t inspect the application-layer data (HTTP, HTTPS headers, etc.).
Layer 7 (Application Layer): Can make distribution decisions based on HTTP headers, cookies, URL path, etc. This is useful for advanced routing and application-aware features.


 How It Works:

1. **Client Sends Request**
   - A user tries to access a website or application.
2. **Traffic Hits Load Balancer**
   - The load balancer receives the request instead of sending it directly to a server.
3. **Distributes Request to Servers**
   - Uses algorithms like **Round Robin, Least Connections, or IP Hash** to decide which server handles the request.
4. **Server Responds**
   - The selected server processes the request and sends the response back via the load balancer.
5. **Maintains Health Checks**
   - Continuously monitors servers; if a server fails, it stops sending traffic to it until it recovers.
  

LOAD BALANCING ALGORITHMS:
## Load Balancing Algorithms

Load balancers use different **algorithms** to decide which server should handle an incoming request.  
Here are the most common ones:

| Algorithm            | How it Works                                                | Use Case / Notes                                     |
|---------------------|-------------------------------------------------------------|----------------------------------------------------|
| **Round Robin**      | Requests are distributed sequentially across servers       | Simple, works well when servers have similar capacity |
| **Least Connections**| Sends request to the server with the fewest active connections | Best for servers with varying workloads            |
| **IP Hash**          | Uses client IP address to determine which server handles the request | Ensures the same client goes to the same server (session persistence) |
| **Weighted Round Robin** | Servers are assigned weights; requests are distributed based on weight | Useful when servers have different capacities     |
| **Random**           | Requests are sent randomly to any server                   | Simple but can be uneven if traffic spikes occur  |
| **Least Response Time** | Sends request to server with the fastest response and least connections | Optimizes for performance and speed               |

---

### Key Points:

- **Round Robin**: Simple and fair but doesn’t consider server load.  
- **Least Connections**: Dynamically balances based on server usage.  
- **IP Hash**: Good for session persistence.  
- **Weighted algorithms**: Useful when servers have different hardware specs.  



CHECKSUMS
## Checksums

A **checksum** is a **small piece of data calculated from a larger set of data**.  
It is used to **verify the integrity of data** when it is stored or transmitted over a network.

### How It Works:

1. **Sender calculates checksum**  
   - Uses a mathematical formula (like addition, XOR, or CRC) on the data.  
   - Appends the checksum to the data before sending.

2. **Receiver calculates checksum**  
   - When the data arrives, the receiver recalculates the checksum on the received data.

3. **Compare Checksums**  
   - If the sender’s checksum matches the receiver’s, the data is considered **intact**.  
   - If they **don’t match**, it indicates **data corruption** during transmission.

---

### Key Points:

- Checksums **detect errors** in data transmission or storage.  
- Commonly used in **networking protocols (TCP/IP), files, and data storage**.  
- Simple checksums detect basic errors; more complex algorithms like **CRC32** or **MD5** provide stronger verification









