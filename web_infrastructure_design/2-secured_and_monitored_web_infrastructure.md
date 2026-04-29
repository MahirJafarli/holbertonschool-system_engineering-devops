First link : https://imgur.com/a/EmnmaGH

Second link : https://excalidraw.com/#json=KopUKditcVjGtRaJ2XIyf,Zz1Ojp8_08EDXa416VUHKA

## Infrastructure Specifics
 - Firewalls: Added to each server to protect the infrastructure by filtering incoming and outgoing traffic based on defined security rules. They prevent unauthorized access to sensitive ports.

 - SSL Certificate: Used to serve traffic over HTTPS. This ensures that data transferred between the user and the load balancer is encrypted, providing confidentiality and integrity.

 - Monitoring: Used to track the health, performance, and availability of the servers. It allows for proactive troubleshooting before a system failure occurs.

 - Data Collection: The monitoring tool (like SumoLogic) uses a client/agent installed on each server that "scrapes" or collects system metrics (CPU, Memory, Disk usage) and logs, then pushes them to a central server.

 - Monitoring QPS: To monitor Queries Per Second, I would configure the monitoring agent to analyze the Nginx access logs, counting the number of HTTP requests processed by the web server per second.

## Identified Issues
 - SSL Termination Problem: Terminating SSL at the load balancer means traffic is only encrypted from the User to the LB. The traffic traveling from the Load Balancer to the Application Servers over the internal network is unencrypted, which is a security risk if the internal network is breached.

 - Single Writable Database: Only the Primary (Main) database can accept "Write" operations. If this specific node fails, the entire application becomes "Read-Only," and users cannot perform actions like signing up or posting content.

 - Resource Competition: Having the Web Server, App Server, and Database on the same machine means they all compete for the same CPU, RAM, and IO. A heavy database query could slow down the web server, leading to poor user experience.
