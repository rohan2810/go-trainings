# Distributed Systems: The Big Picture
#Learning/Udemy/Distributed-Systems

## What are distributed system?
A collection of indecent computers that appear to its users as one 
computer

## Distributed System Characteristics:
1. Concurrency: All servers operate at the same time
2. Independence: Servers run and fail indecent of each other
3. No shared clock: Servers do not share a global clock

> application architecture should evolve around the business model and nit 
around the technology  

## Use case: e-commerce website:
Primary use case:
	* account signup
	* item listing 
	* catalog search
	* checkout and payment
	* shipping, tracking, and delivery
	* feedback, refund, and returns

### Traditional Client/Server model

![](Distributed%20Systems%20The%20Big%20Picture/Screen%20Shot%202022-12-09%20at%2012.53.23%20AM.png)

**Domain Name System (DNS):** A hierarchical and decentralized naming 
system for computers and translates domain names to IP addresses

**Content Delivery Network (CDN):** A collection of distributed servers 
that deliver static pages and other content to a user based on their 
geographical location.

	* **Vertical Scalability**
		* Upgrade hardware and/or network throughput (for eg. Add 
more servers)
		* No application redesign needed
		* works even better with virtual servers
		* CONS:
			* Cost inefficient
			* Hardware limitations
			* Operating system design

	* **Horizontal Scalability**:
		* Run each component of your application on multiple 
servers
		* add/remove servers as needed — autoscaling
		* commodity hardware instead of specialized servers


![](Distributed%20Systems%20The%20Big%20Picture/Screen%20Shot%202022-12-09%20at%201.01.13%20AM.png)

 
## Components of a Distributes System
### Building the front-end layer
#### State management
* User Session
* Memory
* Local files
* Resource locks

> keep your servers stateless. Scale horizontally by adding more servers  

	* Client and server communicate over HTTP
	* HTTP protocol is stateless
	* establish HTTP session with cookies in request and response 
headers
	* CONS:
		* Cookies are sent with every individual request
			* solution: store session data in an external 
datastore
			* For local files, use CDN or an object store

![](Distributed%20Systems%20The%20Big%20Picture/Screen%20Shot%202022-12-09%20at%201.13.17%20AM.png)

![](Distributed%20Systems%20The%20Big%20Picture/Screen%20Shot%202022-12-09%20at%201.13.46%20AM.png)


### Handling business logic with web services
  
> Web services encapsulates the business logic and hides complexity behind 
and API contract  

**Functional Partitioning**: Split a large system into a set of smaller, 
loosely couples and indecent web series - each focusing on a subset of 
functionality of the overall system

![](Distributed%20Systems%20The%20Big%20Picture/Screen%20Shot%202022-12-09%20at%201.41.13%20AM.png)


### Scaling web services:

	* No shared store
		* Use cache, database and messageQueues
	* Stateless servers
		* Scale by adding replica servers (autoscale)
	* Load Balancers
		* Between clients and backend servers
	* Isolate server failures
		* Servers routinely ping load balancer
	* Easy maintained
		* zero downtime update of services
Disadvantages:
	* Distributed Transactions: implementing an operation consisting 
of a set of web service calls that should either fail or pass
	
## Data Layer
Replication:
	* Sychromize state bw multiple servers
	* Scale read throughput and provide higher availibity
	* each server holds an identical copy of data

![](Distributed%20Systems%20The%20Big%20Picture/Screen%20Shot%202022-12-09%20at%201.47.38%20AM.png)

Replication challanges:
	* Introduces complexity
	* Replication laf
	* only applicable for scaling reads

**Sharding (partitioning)**

	* divide dataset into smaller chunks
	* each server processes only a subset of data
	* isolate failure of servers for each other

Sharding key: determines the distribution of the dataset among your 
servers

Sharding challenges:
		* Sharding function can be complex
		* mapping can break
		* querying data across shards
> CAP theorem: states that its impossible to build a distributed system 
that would simultaneously guarantee consistency, availability and 
partition tolerance  

Consistency: all servers see the same data
Availability server can process request even when other servers are down
Partition Tolerance: System is functional even when servers cannot 
communicate

![](Distributed%20Systems%20The%20Big%20Picture/Screen%20Shot%202022-12-09%20at%201.53.40%20AM.png)



## Handling asynchronous communication
**Synchronous Communication**: A call is made to a remote server, which 
blocks until the operation completes
![](Distributed%20Systems%20The%20Big%20Picture/Screen%20Shot%202022-12-09%20at%201.55.16%20AM.png)

**Asynchronous communication**: The caller doesn’t wait for the operation 
to complete before returning

**Asynchronous communication Patterns**
	1. Fire and forget: caller doesn’t care if the operation completes 
or not
	2. Callback: register a callback to be notified when the operation 
completes
	3. Event-based: client emit events. Subscribers react 
independently.

![](Distributed%20Systems%20The%20Big%20Picture/Screen%20Shot%202022-12-09%20at%201.57.22%20AM.png)

Thank you page is shown first then all background activities run

### Message queues

	* Buffers and distributes asynchronous requests
	* messages are platform independent (json, xml)
	* producers and consumers run as separate processes and hosted on 
different servers

Producers:
	* Initiate asynchronous calls
	* creates a message and push it to the queue
	* message format serves as the contract
Message Broker:
	* Provides the following features:
		* Message queuing
		* Persisting
		* routing and delivery
	* Configuration over sutomization
	* support higher throughput and scalability


Consumers:
	* process request asynchrously
	* implemented in the application code:
		* Pull model: the consumer periodically checks for 
messages
		* push model: the consumer opens and keeps the connection 
with the broker
Message Routing:
	* Direct worker queue method:
		* Single work queue identified by name
		* multiple producers nad consumers
		* each message routed to one sonsuner
		* ideal for long running tasks
			* video transcoding
			* data classification
			* image resizing

![](Distributed%20Systems%20The%20Big%20Picture/Screen%20Shot%202022-12-09%20at%202.05.00%20AM.png)


![](Distributed%20Systems%20The%20Big%20Picture/Screen%20Shot%202022-12-09%20at%202.05.17%20AM.png)



