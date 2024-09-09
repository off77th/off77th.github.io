---
layout: post
title: "Dynamo: Amazon’s Highly Available Key-value Store"
date: 2024-09-09 +0200
tags: studying
published: true
---

Second paper, ["Dynamo: Amazon’s Highly Available Key-value Store"](https://www.amazon.science/publications/dynamo-amazons-highly-available-key-value-store){:target="_blank"}. Looks like must-read for all who is interested in Databases design.
> This paper described Dynamo, a highly available and scalable
data store, used for storing state of a number of core services of
Amazon.com’s e-commerce platform. \
... \
The production use of Dynamo for the past year demonstrates that decentralized techniques can be combined to provide a single highly-available system. Its success in one of the most challenging application environments shows that an eventual-consistent storage system can be a building block for highly-available applications.

Key points from the paper:
1. **Core Requirements**:
   - Amazon services demand extreme availability, reliability, and low-latency performance.
   - Traditional databases weren't suitable for Amazon’s needs due to scalability and availability issues, leading to the design of Dynamo.
2. **Design Assumptions and Techniques**:
   - **Decentralized Architecture**: Dynamo avoids centralized control, allowing horizontal scaling by distributing data across nodes without a master node.
   - **Eventually Consistent Model**: The system ensures availability even during partition failures by allowing replicas of data to diverge temporarily, eventually reaching consistency.
   - **High Availability for Write Operations**: Dynamo prioritizes writes over strong consistency, allowing the system to be highly available during network partitions.
3. **Partitioning and Replication**:
   - Dynamo uses consistent hashing to partition data across nodes, ensuring efficient load balancing and scalability.
   - Data is replicated across multiple nodes to ensure fault tolerance and availability, even during node failures.
4. **Consistency and Versioning**:
   - Dynamo allows clients to read potentially stale data, managing conflicts with versioning.
   - Vector clocks are used to maintain version histories, enabling the detection of conflicting updates which can later be resolved using application-specific logic.
5. **Handling Failures**:
   - Dynamo is designed to handle failures seamlessly through techniques like hinted handoff (temporary storage of data on another node) and anti-entropy protocols (merging divergent replicas).
   - It uses a gossip-based protocol to keep track of system membership and to handle node failures.
6. **Sloppy Quorum and Tunable Consistency**:
   - Dynamo offers tunable consistency where developers can balance the trade-off between consistency, availability, and performance by adjusting the number of nodes involved in read/write operations.
   - It implements a “sloppy quorum” mechanism to ensure availability during temporary node failures.
7. **Decentralized and Self-Managing System**:
   - The system can self-manage, automatically rebalancing data as nodes are added or removed, using a gossip protocol to propagate changes.
   - It ensures there is no single point of failure or bottleneck in the system.
8. **Performance and Scalability**:
   - Dynamo was designed to handle Amazon's growing traffic load, scaling horizontally by adding commodity hardware.
   - It provides predictable performance even as the system scales, meeting the needs of a highly interactive, always-on service.

The design decisions highlighted in the paper have influenced numerous distributed systems that came after Dynamo, including modern NoSQL databases like Apache Cassandra and Riak. Dynamo exemplifies how tailored trade-offs in distributed system design can meet the operational demands of large-scale, real-time applications.
