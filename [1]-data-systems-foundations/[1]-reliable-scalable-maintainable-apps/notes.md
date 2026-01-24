# Chapter 1: Reliable, Scalable, and Maintainable Applications

## Types of Software Challenges

We have two types of challenges when it comes to building software:

1. **Data-intensive applications**  
   In this kind of application, the main challenge is handling a huge volume of data.  
   The data is usually complex and changes frequently.

2. **CPU-intensive applications**  
   Here, the capacity of the CPU is the main bottleneck.

→ In this book, we will focus on **data-intensive applications**.

But what is a data-intensive application about?

## Data-Intensive Apps in Action

By a data-intensive application, we are referring to applications that handle the following kinds of operations:

- Storing data so it can be used later
- Remembering processed data results so they can be reused without repeating the same computation (cache databases)
- Sending messages to other processes to handle operations asynchronously (stream processing)
- Processing large amounts of data periodically (batch processing)

Each application usually requires a combination of specific tools.  
We must choose each tool wisely so it handles its task efficiently, as a single tool is rarely sufficient to solve a major problem on its own.

---

## Example of a Data System Combining Multiple Tools

![Example of a data-intensive system](../../diagrams/data-system-example.svg)

Our main goal when building systems is to make them:
**Reliable**, **Scalable**, and **Maintainable**.

---

### Reliability

An application should keep working correctly even when something goes wrong.

A reliable system:
- Performs the expected functionalities
- Performs well under the expected load
- Prevents unauthorized access and abuse
- Anticipates and tolerates manageable faults

#### Why is reliability important?

- Bugs in business systems can cause financial losses and legal risks
- Even in small applications, we should be responsible  
  For example, in an image storage application, users may store their preferred images.  
  It would be unacceptable to face issues such as database corruption or data loss.

Sometimes, however, we are forced to sacrifice reliability due to certain constraints,
such as a low budget or when building an experimental application (all vibe-coded 😉).

### Scalability

Scalability is about how our system is affected by an increase in load.  
For example, if our system works well when a maximum of 10k users are using it, how will it perform if 1M users start using it?  
And how can we add computing resources to handle this additional load? Is it manageable?

One key concept for scalability is **performance**.

We usually think about one of two things:

- Increasing the load parameter while keeping the same system resources:  
  how is the performance affected?

- Increasing the load parameter, and determining how much we need to increase the resources so that performance does not change.

The meaning of **performance** depends on the type of system we are working on.  
For example:
- In a batch processing system, we care about **throughput** (how many records we can process per second)
- In online systems, we care about **response time** (how fast the service responds to requests)


### Maintainability

We should focus on building systems that are easy to understand, modify, and maintain.  
To achieve this, we should pay attention to three main design principles:

- **Operability**: Make it easy to keep the system running smoothly (e.g., CI/CD pipelines, monitoring, logging)

- **Simplicity**: Make the system easy to understand for developers and operators

- **Evolvability**: Make it easy to make changes or updates to the system
