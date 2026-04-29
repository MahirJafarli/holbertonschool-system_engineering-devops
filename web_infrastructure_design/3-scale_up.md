First link : https://imgur.com/a/uJJxQZn

Second link : https://excalidraw.com/#json=JK7A5uShLMoxwZRi8UFLY,pbOV5odRB-K-OM8GnUwjdw

# Why the additional elements?
 - Load-Balancer Cluster (HAproxy): I added a second load balancer configured in a cluster with the first one to eliminate the Single Point of Failure (SPOF). Using a Floating IP, if the primary LB fails, the second one takes over immediately (Failover).

 - Split Web Servers (Nginx): The web servers are now on their own dedicated machines. This allows them to handle incoming traffic and SSL termination without competing for resources with the application logic.

 - Split Application Servers: Moving the codebase to its own server layer ensures that the "business logic" has dedicated CPU and RAM. This makes the system easier to scale horizontally by adding more app nodes.

 - Split Database Servers (MySQL): Databases are resource-intensive. Separating them ensures they have dedicated Disk I/O and prevents other services (like a memory-hungry app) from crashing the database.
