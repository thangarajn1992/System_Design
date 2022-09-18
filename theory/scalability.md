# Scalability

### What is Scalability?

_A service is said to be scalable if when we increase the resources in a system, it results in increased performance in a manner proportional to resources added_. Increasing performance in general means serving more units of work, but it can also be to handle larger units of work, such as when datasets grow.

_An always-on service is said to be scalable if adding resources to facilitate redundancy does not result in a loss of performance_.

#### Performance vs Scalability

One simple way to differentiate them is, if we have a performance problem then our system is slow for single user. If we have a scalability problem, then our system is fast for single user but slow under heavy load.

### Why Scalability is Hard?

* **Scalability cannot be an after thought**: It requires applications and platforms to be designed with scaling in mind, such that adding resources actually results in improving the performance or that if redundancy is introduced the system performance is not adversely affected. Many algorithms that perform reasonably well under low load and small datasets can explode in cost if either requests rates increase, the data-set grows or the number of nodes in the distributed system increases.
* **Handling Heterogeneity:** Resources in the system increase in diversity as next generations of hardware come on line, as bigger or more powerful resources become more cost-effective or when some resources are placed further apart. Heterogeneity means that some nodes will be able to process faster or store more data than other nodes in a system and algorithms that rely on uniformity either break down under these conditions or under-utilize the newer resources.

### Can Good Scalability be achieved ?

* Only if we architect and engineer our systems to take scalability into account.
* For the systems we build we must carefully inspect along which axis we expect the system to grow, where redundancy is required, and how one should handle heterogeneity in this system.
* Make sure that architects are aware of which tools they can use for under which conditions, and what the common pitfalls are.
