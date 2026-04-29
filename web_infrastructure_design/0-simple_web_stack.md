https://excalidraw.com/#json=Fn6O50Xo6bxQiunUs9ZU-,RQX3i6VSzcHlSMXqZtC3kA

## 1. DNS Record Specifics
In this infrastructure, the domain is configured as follows:

 - Domain Name: foobar.com

 - Subdomain: www

 - Record Type: A Record

 - Value: 8.8.8.8

Role: The A Record maps the human-readable hostname (www.foobar.com) directly to the IPv4 address of your server. This allows the user's browser to know exactly which "house" on the internet to visit.

## 2. Issues & SPOF (Single Point of Failure)
Because this is a "Simple Web Stack" where everything lives on one machine, it is highly fragile.

 - SPOF (Single Point of Failure): The entire server itself is a SPOF. If the hardware fails, the power goes out, or the Nginx service crashes, the entire website is offline. There is no redundancy (no "backup" server) to take over the load.

 - Downtime for Maintenance: Whenever you need to update your code, tweak the Nginx configuration, or update the MySQL database version, you often have to restart the services or the server. Because there is only one server, users will experience a "502 Bad Gateway" or "Connection Refused" error during that window.

 - Scalability: This design cannot handle high traffic. If too many users visit www.foobar.com at once, the CPU and RAM of this single server will be overwhelmed, causing the site to slow down or crash entirely.

## 3. Component Definitions (For your notes)
Web Server (Nginx): Receives HTTP requests and acts as a reverse proxy.

 - Application Server: Executes the logic of your codebase (e.g., Python, PHP, or Node.js).

 - Database (MySQL): Provides persistent storage for application data.

 - Communication: The server and user communicate using the HTTP protocol over a TCP/IP connection.
