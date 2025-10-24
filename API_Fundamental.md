                                                                                          API(APPLICATION PROGRAMMING INTERFACE)

At its core, an API is a bunch of code that takes an input and gives you predictable outputs.
Think of an API as a middleman that enables applications to interact without needing direct access to each other's code or database.

Almost every digital service you use today—social media, e-commerce, online banking, ride-hailing apps—all of them are a bunch of APIs working together.

Examples:

Weather API – If you provide a city name as input ("New York"), the API returns the current temperature, humidity, and weather conditions.
Uber Ride API – If you provide a pickup and destination address, the API finds the nearest available driver and calculates the estimated fare.
Python's sorted() API – If you provide a list of numbers ([5, 3, 8, 1]), the API returns the sorted list ([1, 3, 5, 8]).


APIs follow a simple request-response model:

A client (such as a web app or mobile app) makes a request to an API.
The API (hosted on an API server) processes the request, interacts with the necessary databases or services, and prepares a response.
The API sends the response back to the client in a structured format (usually JSON or XML).
![API](https://github.com/anjali22-lgtm/System-Design/raw/44764ba8f9347e505885ba05b0da5820228b142c/api.png)


For example, the Google Maps API always returns coordinates in the same format.
Json:
{   
  "latitude": 40.6892,   
  "longitude": -74.0445 
}
If the API can’t find the location, it provides an error response explaining why.

Json:
{
  "error": "Invalid address format",
  "code": 400 
}

Types of APIs:
![API](https://github.com/anjali22-lgtm/System-Design/blob/7fbc2bb21c545d5b090750725b3c2ed30129201f/type.png)
1. REST API (Representational State Transfer)
Most widely used API type.
Uses HTTP methods like GET, POST, PUT, and DELETE.
Data is exchanged in JSON format.

Stateless – each request is independent of previous ones.

Example:
GET https://api.example.com/users/1

Response:

{
  "id": 1,
  "name": "Anjali",
  "role": "Engineer"
}
✅ Advantages:

Lightweight and easy to use.
Works well with browsers and mobile apps.

⚙️ 2. SOAP API (Simple Object Access Protocol)

Based on XML and follows strict communication standards.
Provides built-in security and reliability.
Commonly used in banking and enterprise systems.

Example SOAP Request:

<soap:Envelope>
  <soap:Body>
    <getUser>
      <userId>1</userId>
    </getUser>
  </soap:Body>
</soap:Envelope>

✅ Advantages:

Highly secure.
Great for complex enterprise environments.

🧩 3. GraphQL API

Developed by Facebook for more flexible data fetching.
Clients can request exactly the data they need.

Example:

{
  user(id: 1) {
    name
    email
  }
}

✅ Advantages:

Prevents over-fetching or under-fetching of data.
Ideal for applications with multiple data sources.

⚡ 4. WebSocket API

Enables real-time, two-way communication between client and server.
Commonly used in chat apps, live dashboards, and games.

Example:
Used in a chat app to instantly send and receive messages through a continuous connection.

✅ Advantages:
Real-time updates.
Faster communication compared to HTTP polling.


How to use API?

Using an API might seem complex at first, but it follows a simple request-response pattern.
Here’s a guide on how to find, access, and interact with an API step by step:
![API](https://github.com/anjali22-lgtm/System-Design/blob/7fbc2bb21c545d5b090750725b3c2ed30129201f/use.png)

Step 1: Find an API to Use
Before using an API, you need to identify the right API for your needs. APIs are available for different services like weather data, finance, social media, etc.
Where to Find APIs?
Public API directories:

RapidAPI – A marketplace for APIs with free & paid options.
Postman API Network – A collection of public APIs.
API List – A fun list of free public APIs.
GitHub’s Public API List – Open-source API collection.
Official API Documentation:

Google APIs
X API
OpenWeather API
Step 2: Read the API Documentation
API documentation explains how to use the API, available endpoints, authentication, and response formats.

Example: The OpenWeatherMap API
The OpenWeatherMap API allows users to fetch real-time weather data. Here's a breakdown of its key components:

API URL
https://api.openweathermap.org/data/3.0/weather?q=city_name&appid=YOUR_API_KEY
Required Parameters:

q: City name (e.g., London)
appid: API Key (required for access)
Step 3: Get API Access (API Key / Authentication)
Most APIs require authentication to prevent unauthorized access and manage usage limits.

Common Authentication Methods:
API Key - A unique key provided by the API service
OAuth 2.0 - Secure login via Google, Github, etc.
JWT (JSON Web Token): Token-based authentication
Basic Authentication: Username + password (Base64 encoded)
Example: Getting an API Key (OpenWeather API)

Sign up at openweathermap
Go to the API keys section and generate a key.
Use the API key in requests: GET "https://api.openweathermap.org/data/2.5/weather?q=London&appid=YOUR_API_KEY"
Step 4: Test the API Using Postman or cURL
Before writing code, test the API to see how it responds.

Option 1: Using Postman (Recommended for Beginners)
Download & install Postman.
Click "New Request", enter the API endpoint URL (https://api.openweathermap.org/data/3.0/weather?q=London&appid=YOUR_API_KEY).
Select GET as the HTTP method.
Click "Send" and view the response in JSON format.
Option 2: Using cURL (For Command Line Users)
You can also test APIs directly from the command line using cURL.

curl -X GET "https://api.openweathermap.org/data/3.0/weather?q=New+York&appid=YOUR_API_KEY"

Step 5: Write Code to Call the API
Now that you’ve tested the API, it’s time to integrate it into your application.

Example: Calling an API in Python
import requests

API_KEY = "YOUR_API_KEY"
CITY = "New York"

url = f"https://api.openweathermap.org/data/3.0/weather?q={CITY}&appid={API_KEY}"

response = requests.get(url)

if response.status_code == 200:
    data = response.json()
    temperature = data['main']['temp']
    print(f"Current temperature in {CITY}: {temperature}°C")
else:
    print(f"Error retrieving data: Status code {response.status_code}")
requests.get(url) – Sends an API request.
response.json() – Converts response to JSON.
if response.status_code == 200 – Checks if the request was successful.
Step 6: Handle Errors & Rate Limits
APIs don’t always return perfect responses. You should handle:

Invalid inputs (e.g., wrong city name).
Authentication errors (e.g., expired API keys).
Rate limits (e.g., exceeding request limits).
Example: Handling API Errors in Python
import requests

API_KEY = "YOUR_API_KEY"
CITY = "New York"

url = f"https://api.openweathermap.org/data/3.0/weather?q={CITY}&appid={API_KEY}"

response = requests.get(url)



                                                                                         DATA FORMATS  

Every time you make an API call, store a file, or send a message in a distributed system, a fundamental question must be answered: "How should this data be represented?"
That’s where data formats come in.

A data format is the contract that defines how information is structured, stored, and exchanged between different parts of a system.
In the world of microservices and large-scale data processing, this choice is not trivial. The right format can make your system fast, efficient, and scalable, while the wrong one can introduce latency, bloat storage costs, and create compatibility nightmares.

The impact of a serialization format is felt across the system:
Performance: How fast can we encode and decode data?
Size: How much space does the data occupy on disk or over the network?
Compatibility: Can systems written in different languages easily understand each other?
Evolvability: How easily can we change the data structure over time without breaking things?


DATA FORMAT- When your app communicates with an API, it sends or receives information.
That information has to be in a specific format — like a language both sides understand.
If you ask an API for user details, it might respond like this:

{
  "name": "Anjali Jamwal",
  "email": "anjali@example.com",
  "role": "student"
}
→ That’s JSON format (JavaScript Object Notation).
So “data format” = the way the data is written, organized, and understood.

1. JSON (JavaScript Object Notation)

Most popular and lightweight data format.
Easy to read and supported by almost all programming languages.

Example:
{
  "id": 1,
  "name": "Anjali Jamwal",
  "email": "anjali@example.com"
}

Used in: REST APIs, Web APIs, Mobile apps.

2. XML (eXtensible Markup Language)

A tag-based format similar to HTML.
Commonly used in older or enterprise APIs (like SOAP).

Example:
<user>
  <id>1</id>
  <name>Anjali Jamwal</name>
  <email>anjali@example.com</email>
</user>
Used in: SOAP APIs, legacy systems.

3. Form Data (application/x-www-form-urlencoded)

Data is sent as key-value pairs in the request body.
Commonly used for HTML form submissions.

Example:
name=Anjali&email=anjali@example.com
Used in: Login forms, contact forms.

4. Multipart/Form-Data

Used when uploading files (images, PDFs, etc.).
Sends both text fields and binary data.
Used in: File upload APIs, media services.

5. YAML (YAML Ain’t Markup Language)

Human-friendly and readable format.
Commonly used for configuration files and API specifications.

Example:
id: 1
name: Anjali Jamwal
email: anjali@example.com
Used in: OpenAPI specs, DevOps tools.

6. CSV (Comma-Separated Values)

Tabular data stored as text, each row separated by a newline.

Example:
id,name,email
1,Anjali Jamwal,anjali@example.com
Used in: Data exports, analytics, reports.

7. Binary Formats (Protobuf / Avro / MessagePack)

Compact and faster to transmit than text-based formats.
Used in internal or microservice communication.
Used in: gRPC APIs, high-performance systems.
![API](https://github.com/anjali22-lgtm/System-Design/blob/7fbc2bb21c545d5b090750725b3c2ed30129201f/data.png)


API Architectural Styles:
![API](https://github.com/anjali22-lgtm/System-Design/blob/7fbc2bb21c545d5b090750725b3c2ed30129201f/archi.png)
1.REST (Representational State Transfer)

Most widely used API style on the web.
Uses HTTP methods like GET, POST, PUT, and DELETE.
Data is usually exchanged in JSON format.
Stateless: each request is independent.

Example:
GET /api/users/1

Used in: Web, mobile, and cloud-based applications.

2. SOAP (Simple Object Access Protocol)

XML-based protocol for exchanging data between systems.
Follows strict standards and uses the WSDL (Web Services Description Language).
Works over multiple protocols — HTTP, SMTP, etc.

Example:
SOAP request wrapped in an XML envelope.
Used in: Enterprise applications, financial systems.

3. GraphQL

Developed by Facebook.
Allows clients to request exactly the data they need — nothing more, nothing less.
Uses a single endpoint (e.g., /graphql).

Example:
{
  user(id: 1) {
    name
    email
  }
}

Used in: Modern web/mobile apps, APIs with flexible queries.

4. gRPC (Google Remote Procedure Call)

High-performance, binary protocol built on HTTP/2.
Uses Protocol Buffers (Protobuf) for data serialization.
Enables bi-directional streaming.

Used in: Microservices, real-time applications, backend-to-backend communication.

5. WebSockets

Enables full-duplex (two-way) communication between client and server.
Keeps the connection open — unlike REST, which opens and closes per request.

Used in: Chat apps, live notifications, gaming, real-time dashboards.

6. Server-Sent Events (SSE)

Allows servers to push data to clients automatically via HTTP.
Lightweight alternative to WebSockets.

Used in: Real-time feeds, stock tickers, live updates.
![API](https://github.com/anjali22-lgtm/System-Design/blob/7fbc2bb21c545d5b090750725b3c2ed30129201f/styles.png)



                                                                                               API GATEWAYS


APIs, or Application Programming Interfaces, are a set of rules and protocols that allows two software applications or services to communicate with each other.
As applications grow in size, the number of APIs increases too. Without the right tools and infrastructure, managing these APIs can quickly become a challenge.
This is where API Gateway comes into play.

An API Gateway acts as a central server that sits between clients (e.g., browsers, mobile apps) and backend services.
Instead of clients interacting with multiple microservices directly, they send their requests to the API Gateway.
The gateway processes these requests, enforces security, and forwards them to the appropriate microservices.
![API](https://github.com/anjali22-lgtm/System-Design/blob/7fbc2bb21c545d5b090750725b3c2ed30129201f/gate.png)


Why do we need API Gateways?
Modern applications, especially those built using microservices architecture, have multiple backend services managing different functionalities.
For example, in an e-commerce service:

One service handles user accounts.
Another handles payments.
Another manages product inventory.

Without an API Gateway:

Clients would need to know the location and details of all backend services.
Developers would need to manage authentication, rate limiting, and security for each service individually.

With an API Gateway:

Clients send all requests to one place – the API Gateway.
The API Gateway takes care of routing, authentication, security, and other operational tasks, simplifying both client interactions and backend management.


Core Features of an API gateways:
API Gateways are powerful because they provide a central layer of control and management over multiple backend services. Here are the key features:

1. Request Routing

Directs incoming client requests to the appropriate backend service.
Supports URL-based, header-based, or parameter-based routing.
Can also route traffic to different service versions (blue-green deployments).

2. Authentication & Authorization

Validates client identity (e.g., API keys, OAuth tokens, JWT).
Ensures only authorized clients can access certain APIs.

3. Load Balancing

Distributes client requests evenly across backend services.
Improves performance and availability.

4. Rate Limiting & Throttling

Limits the number of requests a client can make in a given time frame.
Prevents misuse and protects backend services from overload.

5. Caching

Stores frequently requested responses for faster delivery.
Reduces latency and load on backend services.
![API](https://github.com/anjali22-lgtm/System-Design/blob/7fbc2bb21c545d5b090750725b3c2ed30129201f/cache.png)

6. Protocol Translation

Converts requests/responses between different protocols:
HTTP ↔ WebSocket
HTTP ↔ gRPC
Allows heterogeneous systems to communicate smoothly.

7. Logging & Monitoring

Tracks metrics like request count, response time, and error rate.
Helps in debugging, auditing, and performance optimization.

8. Security & Traffic Management

Protects services from attacks like DDoS, SQL injection, and XSS.
Can enforce encryption via HTTPS/TLS.

9. API Composition / Aggregation

Combines responses from multiple services into a single response for the client.
Reduces the number of requests a client needs to make.

10. Analytics & Insights

Provides detailed insights into API usage patterns.
Helps identify bottlenecks, high-traffic endpoints, and optimization opportunities.


⚙️ How Does an API Gateway Work?

An API Gateway acts as a single entry point between clients and backend services, managing all incoming requests, routing them appropriately, and handling cross-cutting concerns like security, caching, and rate limiting.

Step-by-Step Workflow

Client Sends Request:
A client (web app, mobile app, or another service) sends a request to the API Gateway instead of calling multiple backend services directly.

Request Routing:
The gateway analyzes the request (URL, headers, parameters) and routes it to the appropriate backend service.

Example:
/api/user → User Service
/api/order → Order Service


Authentication & Authorization:
The gateway verifies if the client is allowed to access the requested API.

Can use API keys, JWT tokens, or OAuth.

Rate Limiting & Throttling:
Controls the number of requests from a client to prevent abuse and ensure system stability.

Protocol Translation (if needed):
Converts requests/responses between different protocols (HTTP ↔ WebSocket, HTTP ↔ gRPC).

Aggregation & Response Handling:
If required, the gateway aggregates responses from multiple backend services into a single response for the client.

Caching (Optional):
Frequently requested data can be cached at the gateway to improve performance.

Logging & Monitoring:
Tracks request metrics, errors, and performance to provide analytics and debugging insights.
Send Response Back to Client

After processing and any aggregation, the final response is sent back to the client.
Visual Example
Client → API Gateway → [User Service, Order Service, Payment Service]
           |→ Auth & Security
           |→ Rate Limiting
           |→ Caching
           |→ Monitoring & Logging
           ![API](https://github.com/anjali22-lgtm/System-Design/blob/7fbc2bb21c545d5b090750725b3c2ed30129201f/bal.png)



                                                                                            RATE LIMITING 


Rate limiting helps protects services from being overwhelmed by too many requests from a single user or client.
1. Fixed Window Rate Limiting

Counts requests in fixed time intervals (e.g., per minute, per hour).
Example: Max 100 requests per minute.
Pros: Simple to implement.
Cons: Can allow bursts at window edges (client sends 100 requests at the end of one minute and 100 more at the start of the next).

2. Sliding Window Rate Limiting

Tracks requests in a rolling window instead of fixed intervals.
Example: Max 100 requests in the last 60 seconds, no matter when the 60-second period starts.
Pros: Smoothes bursts, more accurate control.
Cons: Slightly more complex to implement.

3. Token Bucket

Each client has a bucket of tokens.
Each request consumes a token.
Tokens refill at a constant rate over time.
Example: 10 tokens per second; if bucket is empty, requests are rejected.
Pros: Allows bursts of requests while maintaining a steady average rate.

4. Leaky Bucket

Requests enter a queue (bucket) and are processed at a fixed rate.
Overflow requests are dropped.
Pros: Smooths traffic and prevents overload.
Cons: Requests exceeding the limit are lost.

5. Dynamic Rate Limiting (Adaptive)

Adjusts the allowed rate based on server load or client behavior.
Example: Reduce request limits during high traffic periods.
Pros: Efficiently manages traffic and ensures system stability.
![API](https://github.com/anjali22-lgtm/System-Design/blob/7fbc2bb21c545d5b090750725b3c2ed30129201f/rate.png)



                                                                                              IDEMPOTENCY


Imagine you're making a purchase from an online store.
You hit "pay" but the screen freezes, and you're unsure if the payment went through.
So, you refresh the page and try again.

Behind the scenes, how does the system ensure you aren’t accidentally charged twice?
This scenario highlights a common problem in distributed systems: handling repeated operations gracefully.

The solution to this problem lies in the concept of idempotency.
In this blog, we'll explore what idempotency is, why it matters, how to implement it, challenges, considerations and best practices to ensure robust and reliable systems.


What is Idempotency?
Idempotency is a property of an operation where performing it multiple times has the same effect as performing it once.
In simpler words, no matter how many times a request is sent, the result on the server remains the same.
![API](https://github.com/anjali22-lgtm/System-Design/blob/7fbc2bb21c545d5b090750725b3c2ed30129201f/idem.png)


Why its Matter?
.Ensures reliability in APIs, especially when network errors or retries occur.
.Prevents duplicate actions, like double payments or creating multiple accounts.
.Critical for safe retries in distributed systems.


Challenges and Considerations:

While idempotency is powerful, it comes with its own set of challenges:
Performance Overhead: Storing idempotency keys or checking for duplicate operations can add overhead and increase the overall latency.
State Management: Idempotency often requires maintaining state, which can be challenging in stateless architectures.
Distributed Systems: Ensuring idempotency across distributed systems can be challenging and may require distributed locking or consensus algorithms.
Time Window: How long should idempotency guarantees be maintained? Forever, or for a limited time?
Database Constraints: Not all operations are idempotent by default; unique constraints or upsert logic may be necessary to avoid duplication.
