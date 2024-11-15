# System Design and Scalability

Step 1: Scope the Problem
- Define the Core Requirements: Clarify the problem and confirm what you're being asked to design
- Identify Key Features: Break down major functions or use cases (e.g., URL shortening, link retrieval, and analytics for a TinyURL service)
- Clarify Optional Details: Ask about customization needs (e.g., user-defined URLs), data persistence (e.g., expiration policies), and additional features like user accounts or link management
- List Key Use Cases: Outlining user actions should help to structure the design around real usage

Step 2: Make Reasonable Assumptions
- its okay to make reasonable assumptions (when necessary) (e.g., designing for a max of one million URLs per day)
- assumptions made rely heavily on context and take some "product-sense"
- discuss your thoughts and confirm assumptions with your interviewer

Step 3: Draw the Major Components
- utilise the whiteboard
- draw a diagram of the system's major components
- walk through your system from end-to-end to provide flow
- explify the flow with a user action (e.g., a user enters a new URL, what happens?)

- Step 4: Identify the Key Issues
- What will be the bottlenecks or major challenges in the system?
- Interviewers will often provide hints / guidance in this section, make note of comments

Step 5: Dedesign for the Key Issues
- Once the constraints and concerns have been identified, adjust your design  (this could be a major or minor redesign of the system)
- Maintain use of the whiteboard / diagram drawing
- Be open about limitations. Your interviewer will most likely be aware of them so its best to communicate that you're on the same page 

---

Key Concepts:

Horizontal vs. Vertical Scaling
- a system can be scaled in two ways:
    - vertical scaling: increasing resources of a specific node (e.g., additional memory to a server to improve its ability to handle load changes)
    - horizontal scaling: increasing the number of nodes (e.g., increasing the number of servers, distributing traffic / load)

Load Balancer
- allows systems to distribute the load evenly so that one server doesn't crash and take down the whole system
- to do this, it requires the building of a network of cloned servers that all have essentially the same code and access to the same data

Database Denormalization and NoSQL
- table joins in relational databases become slow in relation to the size of the tables being joined
- denormalization: means adding redundant information into a database to speed up reads (e.g., putting data that would normally belong in its own table, populating an existing table where the query would orinate from to prevent table joins)
- another option is to use a NoSQL database
    - doesnt support table joins since there arent "tables" 
    - designed to scale better

Database Partitioning (Sharding)
- splitting data across multiple machines while ensuring you have a way of figuring out which data is on which machine
- Vertical Partitioning: partitioning by feature (e.g., one instance for tables relating to profiles, another for messages, etc.)
- Key-Based (or Hash-Based) Partitioning: uses some part of the data (e.g. an ID) to partition by creating a hash and applying `mod(key, n)` to see which partition the record falls into
- Directory-Based Partitioning: maintain a lookup table for where the data can be found. Constant access to this lookup table can impact performance

Caching
- In-Memory: simple key-value pairing that sits between the application layer and the data store
- When an application requests data, it first tries the cache. If the cache is not valid or doesn't contain the key, it will then look in the data store

Asynchronous Processing and Queues: slow operations should be executed asynchronously 

Network Metrics
    Bandwith: the maximum amount of data that can be transferred in a unit of time (e.g., bits per second)
    Throughput: the actual amount of data that is transferred 
    Latency: how long it takes data to go from a source point to its destination


MapReduce: a program that is typically used to process large amounts of data
- Map step: takes in some data and emits a <key, value> pair
- Reduce step: takes a key and a set of associated values and "reduces" them in some way (this can be recursively reduced further)


Considerations:
- Failures: Essentially any part of a system can fail. You'll need to plan for many or all of these failures.
- Availability and Reliability: Availability is a function of the percentage of time the system is operational. Reliability is a function of the probability that the system is operational for a certain unit of time.
- Read-heavy vs. Write-heavy: Whether an application will do a lot of reads or a lot of writes impacts the
design. If it's write-heavy, you could consider queuing up the writes (but think about potential failure here!). If it's read-heavy, you might want to cache. Other design decisions could change as well.
- Security: Security threats can, of course, be devastating for a system. Think about the types of issues a system might face and design around those