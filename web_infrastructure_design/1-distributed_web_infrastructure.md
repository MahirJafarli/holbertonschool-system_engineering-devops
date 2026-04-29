First link : https://imgur.com/a/V5uqXvS

Second link : https://excalidraw.com/#json=99qoZATs5EXNmynH2qCo-,R44UwWV7xsJgfl3aIQvmOQ

## 1. Infrastructure Specifics
 - Why the extra elements?: We added an HAproxy Load Balancer to distribute traffic and a second server to provide redundancy. This ensures that if one web server fails, the site stays online.

 - Load Balancer Algorithm: Configured with Round Robin. This algorithm rotates incoming requests between Server 1 and Server 2 equally, ensuring neither is overwhelmed.

 - Active-Active vs. Active-Passive: This is an Active-Active setup. Both servers are handling traffic simultaneously. In an Active-Passive setup, one server remains idle and only takes over if the active one fails.

 - Database Primary-Replica (Master-Slave): The Primary node handles all "Write" operations (saving data), while the Replica node synchronizes with the Primary and handles "Read" operations. This balances the database load.

## 2. Issues with this Infrastructure
 - SPOF (Single Point of Failure):

 - The Load Balancer is a SPOF; if it fails, no traffic reaches the servers.

 - The Primary Database is a SPOF; if it fails, the site cannot perform any "Write" actions.

 - Security: There is no Firewall to protect the servers from attacks, and no HTTPS certificate, meaning data is transmitted unencrypted (vulnerable to sniffing).

 - Monitoring: There is no monitoring system (like Nagios or Datadog) to alert us if a server is healthy or failing.
