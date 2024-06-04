---
title: Designing Data Intensive Applications
---

# Chapter 1

## Most Important System Concerns

* Reliability
  * System works correctly
* Scalability
  * Grows when data volume, traffic volume, or complexity grows
* Maintainability
  * Ease of maintaining existing behavior and adaptability to new use cases

The author lumps Databases and Message Queues into one broad term "Data Systems" because the lines between the two are getting blurred.

* Data stores like Redis are are used as message queues
* Message queues like Apache Kafka now have database-like durability guarantees

Imagine you were a system designer, 

* How would you ensure data is correct and complete? (even when failures happen)
* How would you ensure fast performance?
* How would you scale?
* What would an API for the service look like?

Fault vs Failure

* A fault is when a component deviates from spec
* A failure is when the system stops providing the service to the user (impossible for probability of a failure to reach 0)

The goal is to prevent faults from becoming failures

Many bugs are actually the fault of improper error handling

Systematic software errors are hard to anticipate and can cause failure across nodes. Software errors cause more failures than hardware faults

Examples of software errors

* Bugs in the system kernel that happen because of a leap second on June 30, 2012
* Runaway process takes up memory, CPI, disk space, network
* Dependencies become unresponsive or corrupt resources
* Cascading failure (small fault causes bigger faults)

Software faults are mitigated by

* Thinking carefully about assumptions and interaction
* Testing
* Process isolation
* Letting processes crash and restart
* Measure and monitor system behavior
* Can run TPS checks to ensure no discrepancies

Minimize human error (like bad config changes) by

* Designing great API's and limit access/design good UI's to help admins make good choices (don't make too restrictive)
* Create sandbox for devs to mess with and experiment
* Test thoroughly (cover corner cases)
* Make rollbacks easy
* Setup good monitoring/telemetry

Twitter has a fan out problem, when a user requests their homepage there are two ways to get tweets:

1. Lookup each person they follow, find all tweets from each of those users, and merge them sorted by time
1. Cache the results of each user's homepage. When a user posts, lookup each person who follows the user that posted and insert the new post into each timeline cache. (This is precompute)

Question: Why did twitter go with approach 1 for celebrities?

In the case of a celebrity, a user pulls the celebrities tweet at the time of checking the homepage. Otherwise, the celebrity's tweet would be cached for all of their followers and millions of caches would need to be updated.

## Latency vs Response Time

* **Latency:** The duration that the request waits to be handled
* **Response Time:** What the client sees (including network delays and queuing delays)
* **Service Time:** Actual time the service takes to process the request

Response time is a distribution of measurable values. 

* The arithmetic mean is not a good measure of response time because it does not tell you how many users actually experienced that delay.
* We use the median (p50) because it lets us know half of all users had a response time less than 200ms (for example)
* High percentiles are known as *tail latencies*and are tracked by companies like Amazon

Amazon uses the 99.9th percentile to understand the experience of customers with the most data (possibly the most valuable customers), however the 99.99th percentile does not have a lot of benefit and is too expensive to improve when latency can be out of your control.

High response time percentiles are often caused by **queueing delays**.

* Ex: a small number of long requests block subsequent requests

Because of this, it is important to measure **Client Side** response times (the server may be processing requests quickly but if they are blocked the response time will suffer)

It is also important that load tests do not wait for a request to finish before sending the next one, otherwise tests may have queues shorter than reality.

**Tail Latency Amplification** can occur when a single end-user request has multiple calls. If just one of these calls is slow the entire response time increases.

The naïve way to calculate response times over a given period of time is to keep a list of response times in a given window and sort the list every minute.

* Do not average percentiles, instead add response time data to histograms

**Scaling up (vertical scaling)**: moving to more powerful machines
**Scaling out (horizontal scaling)**: distributing the load across multiple smaller machines

**Question:** "Good architectures usually involve a pragmatic mixture of approaches." (referring to both Scaling up and Scaling out). When would be an example of a time when it is better to choose scaling up vs when it is better to scale out? What would be the tradeoff (outside of cost) for each approach? (Section: “Approaches for Coping with Load”)

## Maintenance Design Principles

* Operability: Make it easy for things to continue running smoothly
* Simplicity: Make it easy for new engineers to understand the system (by removing complexity when possible)
* Evolvability: Make it easy for engineers to change the system and adapt it to new use cases

 > 
 > “good operations can often work around the limitations of bad (or incomplete) software, but good software cannot run reliably with bad operations”

Operations teams should

* Monitor health of system and restore services when they go out
* Root cause problems like system failures or bad performance
* Keep things up to date/security patched
* Keep tabs on how systems affect each other
* Anticipate future problems (capacity planning)
* Create good config management and deployment tools
* Complex maintenance like migrations or moving from one platform to another
* Maintain security
* Define processes to make operations predictable and keep the env stable
* Preserve knowledge of the system (even when people leave)

Thoughts: I've been warned about over abstracting and I'm curious whether this is a good use of an abstraction. Wouldn't it be better to try to simplify the complex behavior to make it more understandable with helper functions/microservices rather than abstracting?

Referring to this section

 > 
 > “One of the best tools we have for removing accidental complexity is abstraction. A good abstraction can hide a great deal of implementation detail behind a clean, simple-to-understand façade. A good abstraction can also be used for a wide range of different applications. Not only is this reuse more efficient than reimplementing a similar thing multiple times, but it also leads to higher-quality software, as quality improvements in the abstracted component benefit all applications that use it.”

---

# Chapter 2

## Data Models and Query Languages

Most applications are made by layering one data model on another

Ask yourself:

 > 
 > "How is each layer represented in terms of the next lower layer"

Example of how to think in layers

* An app developer modeling real people, organizations, goods, actions which are manipulated by APIs
* When storing these data structures, store as JSON or XML
* JSON or XML are represented by bytes, memory, disk, network
* Those bytes are represented by electrical currents, pulses of light, magnetic fields, etc.

Abstractions and layers allow people to work together effectively. 

## Relational Model vs Document Model

Best-known Data Model - SQL

**Relational Database:** 

 > 
 > In a relational database, each row in the table is a record with a unique ID called the key. The columns of the table hold attributes of the data, and each record usually has a value for each attribute, making it easy to establish the relationships among data points.

Relational database usage started in the 60s and 70s for mundane use cases like invoicing, payroll, reporting, banking transactions, airline reservations, etc.

Most of what is built today still relies on Relational Databases (As of when this book was written in 2017, lol dang I was a junior in high school)

## The Birth of NoSQL

Driving forces behind NoSQL

* A need for better scalability than Relational Databases (RD) (large datasets/high write throughput)
* Preference for free/open source software over commercial databases
* Some queries are not well supported by RD
* Restrictiveness of RD's schemas, desire for dynamic/expressive data models

Note: JSON is a type of *Document Database*

## Object-Relational Mismatch

If data is stored in a relational database, there is a translation between the database model of rows, tables, and columns, to the objects in application code. This disconnect is called *impedance mismatch*.

Object-relational mapping (ORM) reduce the code in these translation layers, but there are still differences between the two models (relational and application code).

JSON has the advantage of having better *locality* than multiple relational databases. To query relational databases with multiple tables, messy joins or multiple queries are necessary. JSON however only requires a single query.

## Many-to-One and Many-to-Many Relationships

Sometimes having an ID with fixed options for locations or jobs is better to ensure

* Consistency
* No Ambiguity for options with identical names
* Ease up updating
* Localization support
* Better Search

Using an ID also reduces value duplication. Instead of storing copies of the value, you can store the value with an ID and use the ID to refer to the single instance of the value. Removing duplications is the idea behind *normalization* in databases.

Normalizing data requires *many-to-one* relationships

* This does not fit nicely into the document model
* Support for joins in document databases are often weak

If your database does not support joins, you need to emulate a join in application code by making multiple queries.

Even if you design your application to not need joins and have a perfect document model, data has a tendency to become more interconnected over time.

The most popular database in the 1970s for business data was IBM's *Information Management System (IMS)*. This used a *hierarchical model* which has many similarities to JSON. All data are records nested within records. This worked well for 1->Many but not for Many->Many and no join support.

This was solved with the *Relational Model* and with the *Network Model*.

## The Network Model

The Network Model/Conference on Data Systems Languages (CODASYL) Model both used a hierarchical model with every record having exactly 1 parent in the CODASYL Model and multiple parents in the Network Model.

The way queries were performed on these models involved "pointers" that followed a path from root record along a chain of links. This is called an *access path* and made queries difficult. If you did not have the exact path to the data you were looking for it would be difficult with a Hierarchical Model or the Network Model.

## The Relational Model

A relation: A table with a collection of rows

A query optimizer will decide which parts of the query to execute in which order and which indexes to use. This is effectively an "access path" but it is dynamic because it is made automatically by the query optimizer.

## Schema Flexibility in the Document Model

JSON and other Document Models have implicit schemas that are sometimes called *schemaless* but a better term is *schema on read* which is where the schema Is interpreted when the data is read. Relational databases are typically *schema on write* and have an explicit schema and the database ensures the data conforms to the schema 

This is similar to dynamic runtime type checking vs static compile time type checking.
