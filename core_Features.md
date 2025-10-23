CORE FEATURES

System design focuses on creating scalable, efficient, and maintainable systems.  
Below are some **core features** that every system design must consider

1.Scalability - It is the property of a system to handle a  growing amount of load by adding resources to the system.
Example: Load balancers, horizontal scaling.

Question arises how system can grow?
Growth in users base
Growth in features
Growth in large volume of data
Growth in complexity

HOW TO SCALE A SYSTEM?
Scaling a system effectively is one of the most critical aspects of satisfying non-functional requirements in system design. 
Scalability, in particular, is often a top priority. Below, we explore various strategies to achieve scalable system architecture.

Decomposition:
Decomposition involves breaking down requirements into microservices. The key principle is to divide the system into smaller, independent services based on specific business capabilities or requirements.
Each microservice should focus on a single responsibility to enhance scalability and maintainability.


Vertical Scaling:
This means adding more power to your existing machines by upgrading server with more RAM, faster CPUs, or additional storage.
It's a good approach for simpler architectures but has limitations in how far you can go.


Horizontal Scaling:
This means adding more machines to your system to spread the workload across multiple servers.
It's often considered the most effective way to scale for large systems.

Example: Netflix uses horizontal scaling for its streaming service, adding more servers to their clusters to handle the growing number of users and data traffic.


Load balancing:
Load balancing is the process of distributing traffic across multiple servers to ensure no single server becomes overwhelmed.

Example: Google employs load balancing extensively across its global infrastructure to distribute search queries and traffic evenly across its massive server farms.


Caching:
Caching serves to improve query read performance by storing frequently accessed data in faster memory storage, such as in-memory caches. 
Popular tools like Redis or Memcached can effectively store hot data to reduce database load.

Example: Reddit uses caching to store frequently accessed content like hot posts and comments so that they can be served quickly without querying the database each time.


Content Delivery Networks (CDNs):
CDN distributes static assets (images, videos, etc.) closer to users. This can reduce latency and result in faster load times.

Example: Cloudflare provides CDN services, speeding up website access for users worldwide by caching content in servers located close to users.


Microservice Architecture:
Micro-services architecture breaks down application into smaller, independent services that can be scaled independently.
This improves resilience and allows teams to work on specific components in parallel.

Example: Uber has evolved its architecture into microservices to handle different functions like billing, notifications, and ride matching independently, allowing for efficient scaling and rapid development.


Auto Scaling:
Auto-Scaling means automatically adjusting the number of active servers based on the current load.
This ensures that the system can handle spikes in traffic without manual intervention.

Example: AWS Auto Scaling monitors applications and automatically adjusts capacity to maintain steady, predictable performance at the lowest possible cost.


Multi-region Deployment
Deploy the application in multiple data centers or cloud regions to reduce latency and improve redundancy.

Example: Spotify uses multi-region deployments to ensure their music streaming service remains highly available and responsive to users all over the world, regardless of where they are located.


2.Availabilty:
Availability refers to the proportion of time a system is operational and accessible when required.
It is usually expressed as a percentage, indicating the system's uptime over a specific period.

The formal definition of availability is:
Availability = Uptime / (Uptime + Downtime)

Uptime: The period during which a system is functional and accessible.

Downtime: The period during which a system is unavailable due to failures, maintenance, or other issues.




3.Reliability-In simple terms, reliability is the ability of a system to perform its intended function consistently over time.
A reliable system is one that:

Remains operational: It continues to work even when parts of it fail.
Recovers quickly: It can bounce back from errors or unexpected events.
Meets expectations: It delivers a consistent user experience, regardless of external factors.

Why reiability matters?
1. Continuous Availability  
Hardware failures, network drops, or software crashes are common in large-scale systems.  
Reliability ensures that the **system stays available** and users experience minimal disruption.  
> Example: When you upload a photo to Instagram, your data remains safe even if one storage server fails — because it’s replicated across multiple nodes.

---

 2. Builds User Trust  
Users rely on systems that **work whenever they need them**.  
Frequent crashes or downtime destroy user confidence.  
That’s why platforms like Google, Netflix, and Amazon invest heavily in reliability engineering.

---

3. Prevents Data Loss  
Reliable systems ensure **data remains safe** despite failures.  
They use:
- Data replication  
- Backups  
- Atomic transactions  

> Example: In online banking, transaction data must never be lost — even if servers crash.

---

 4. Supports Scalability  
If your base system is unreliable, scaling it will only multiply problems.  
Reliability forms the **foundation of scalable architecture**.

---

 5. Reduces Maintenance Cost  
Reliable systems require **less manual recovery** and fewer emergency fixes, saving time and operational cost.

---

### 🧰 Techniques to Improve Reliability
- **Redundancy:** Multiple servers/components perform the same job.  
- **Load Balancing:** Distributes traffic evenly to prevent overload.  
- **Health Checks:** Continuously monitor system components.  
- **Automatic Recovery:** Restart failed services automatically.  
- **Consensus Algorithms:** (e.g., Raft, Paxos) for consistent distributed state.  
- **Monitoring & Alerts:** Detect and respond to failures quickly.



CONSISTENCY MODELS:
In distributed systems, consistency models define how data updates are shared and viewed across multiple nodes. They set the rules for synchronization, ensuring users and applications interpret data changes 
correctly. 
Depending on the approach, strict or relaxed systems balance reliability, availability, and performance.

TYPES:
1.Strong Consistency- In a strongly consistent system, all nodes in the system agree on the order in which operations occurred. Reads will always return the most recent version of the data, when an update occurs on one server, 
this model makes sure every other server in the system reflects this change immediately.
This model provides the highest level of consistency, but it can be slower and require more resources in a distributed environment since all servers must stay perfectly in sync.

2.Weak Consistency- A weakly consistent system provides no guarantees about the ordering of operations or the state of the data at any given time. Clients may see different versions of the data depending on which node they connect to. 
This model provides the highest availability and scalability but at the cost of consistency.

3. Sequential Consistency Model- It is a consistency model in distributed systems that ensures all operations across processes appear in a single, unified order. In this model, every read and write operation from any process appears to happen in sequence, regardless of where it occurs in the system.
 Importantly, all processes observe this same sequence of operations, maintaining a sense of consistency and order across the system

4.Causal Consistency- The Causal Consistency Model is a type of consistency in distributed systems that ensures that related events happen in a logical order. In simpler terms, if two operations are causally related (like one action causing another), 
the system will make sure they are seen in that order by all users. However, if there’s no clear relationship between two operations, the system doesn’t enforce an order, 
meaning different users might see the operations in different sequences.


🧠 Why Consistency Models Appear in System Design
💡 1. Because Data is Stored in Multiple Places

In small systems, data is stored in one database, so it’s easy to keep everything consistent.
But in large-scale distributed systems (like WhatsApp, Netflix, or Google Drive), data is stored on many servers across different locations.

➡️ Example:
If you send a WhatsApp message, the same message may be stored on:
Your device

WhatsApp servers in different regions
The receiver’s device

Keeping all those copies the same at all times becomes challenging — and that’s where consistency models come in.

⚙️ 2. Because Perfect Consistency Slows Things Down
Imagine every read/write operation must update all servers instantly to keep perfect consistency.
That would mean:

Every write must wait for confirmation from all replicas.

Latency increases, especially if servers are far apart geographically.

So designers often trade a bit of consistency for faster performance and better availability — depending on what’s most important for the system.
That’s why different consistency models (like strong consistency, eventual consistency, etc.) were developed.

⚖️ 3. Because of the CAP Theorem

The CAP theorem states that a distributed system can only guarantee two of the following three at once:

C – Consistency (all nodes see the same data)

A – Availability (system always responds)

P – Partition Tolerance (system works even if communication between nodes fails)


CAP Theorem:
CAP stands for Consistency, Availability, and Partition Tolerance, and the theorem states that:

It is impossible for a distributed data store to simultaneously provide all three guarantees.

Consistency (C): Every read receives the most recent write or an error.
Availability (A): Every request (read or write) receives a non-error response, without guarantee that it contains the most recent write.
Partition Tolerance (P): The system continues to operate despite an arbitrary number of messages being dropped (or delayed) by the network between nodes.

Beyond CAP: PACELC
While CAP is foundational, it doesn't cover all scenarios.

Daniel Abadi proposed the PACELC theorem as an extension by introducing latency and consistency as additional attributes of distributed systems.

If there is a partition (P), the trade-off is between availability and consistency (A and C).
Else (E), the trade-off is between latency (L) and consistency (C).
This theorem acknowledges that even when the system is running normally, there's a tradeoff between latency and consistency.

In conclusion, the CAP Theorem is a powerful tool for understanding the inherent trade-offs in distributed system design. It's not about choosing the "best" property, but rather about making informed decisions based on the specific needs of your application.

By carefully evaluating the CAP trade-offs, you can architect robust and resilient systems that deliver the right balance of consistency, availability, and partition tolerance.



CONSISTENT HASHING
In a distributed system where nodes (servers) are frequently added or removed, efficiently routing requests becomes challenging.
A common approach is to use hash the request and assign it to a server using Hash(key) mod N, where N is the number of servers.

However, this method is highly dependent on the number of servers, and any change in N can lead to significant rehashing, causing a major redistribution of keys (requests).
Consistent hashing addresses this issue by ensuring that only a small subset of keys need to be reassigned when nodes are added or removed.

How Consistent Hashing Works?
Consistent hashing is a distributed hashing technique used to efficiently distribute data across multiple nodes (servers, caches, etc.).
It uses a circular hash space (hash ring) with a large and constant hash space.
Both nodes (servers, caches, or databases) and keys (data items) are mapped to positions on this hash ring using a hash function.

Unlike modulo-based hashing, where changes in the number of nodes cause large-scale remapping, consistent hashing ensures that only a small fraction of keys are reassigned when a node is added or removed, making it highly scalable and efficient.

Example: Constructing a Hash Ring
Step 1: Define nodes
Nodes = [Node A, Node B, Node C]

Step 2: Hash the nodes

Assume we use a simple hash function (hash(node) % 360 for degrees):

Node	Hash (position on ring)
A	50
B	180
C	300
Step 3: Draw the ring
 0                                         360
 |-------------------------------------------|
          A(50)         B(180)       C(300)

Step 4: Assign keys

Keys: k1, k2, k3, k4

Hash them:

k1 → 20
k2 → 60
k3 → 190
k4 → 310


Assign clockwise to next node:

k1 → A(50)
k2 → B(180)
k3 → C(300)
k4 → A(50)   (wrap around the ring)


✅ Notice: If Node B fails, only keys between Node A → B move to the next node (Node C). Others stay on their nodes.

4️⃣ Visualization
          (A=50) k1,k4
         /     
        |      
        |       
        |         
        |        
        |         
        |         
        |        
(B=180) k2
        |
        |
        |
        |
(C=300) k3
        |
        |
       360/0

5️⃣ Advantages of Hash Ring
Minimal disruption when nodes are added/removed
Balanced key distribution
Easy to scale large systems



LATENCY Vs THROUGHPUT

Latency is the time it takes for a single request to travel from the source to the destination and get a response.
It’s basically the delay in your system.
Measured in milliseconds (ms) or seconds.

⚡ Examples:

Sending a message on WhatsApp: ~50ms latency
Loading a webpage: 100–200ms latency

🧠 Why Latency Matters:

Users feel slow or laggy experience if latency is high.
Real-time applications (gaming, messaging, video calls) require low latency.

Throughput
💡 Definition:

Throughput is the amount of work a system can do in a given amount of time.
Usually measured as requests per second (RPS), transactions per second, or data per second.
It shows the capacity of your system.

⚡ Examples:

WhatsApp handles millions of messages per second
Netflix streams thousands of videos per second

🧠 Why Throughput Matters:

High throughput ensures the system can serve many users simultaneously.
Throughput is especially important for batch processing, data pipelines, or high-traffic APIs.


Relationship Between Latency and Throughput:

High throughput doesn’t always mean low latency.
If a system tries to handle too many requests at once, latency may increase.

Visualization:
System Capacity
|
|       Low Latency + High Throughput
|      ●
|
|       High Throughput but Higher Latency
|      ●
|
|________________________ Time / Requests

Goal: Design systems that balance throughput and latency according to user needs.




