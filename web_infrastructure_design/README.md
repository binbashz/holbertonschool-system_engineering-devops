task 0

The domain name www.foobar.com that the user enters in his browser to access the website is displayed at the top.

The DNS request is then sent to the DNS server that resolves the domain name to the server's IP address.

The web server (Nginx) receives the HTTP request and handles the static requests directly, returning the HTML files, CSS, images, etc., to the user.

Dynamic requests are sent to the application server, which is responsible for processing the application logic and generating dynamic responses.

The application server can interact with the database (MySQL) to obtain or store data needed for the web application.

Finally, the response is sent back to the web server and then to the user, who views the website in his browser.





task 01

I successfully designed a three-server web infrastructure on a whiteboard for hosting the website www.foobar.com. The infrastructure includes 2 servers, 1 web server (Nginx), 1 application server, 1 load balancer (HAProxy), 1 set of application files (code base), and 1 database (MySQL).

Specifics of the Infrastructure:

Addition of Components: Each component was added to fulfill specific requirements. The servers provide the hardware and resources, the web server handles incoming requests, the application server executes dynamic content, the load balancer distributes the load, the application files contain the code base, and the database stores and manages website data.
Load Balancer Distribution Algorithm: The load balancer (HAProxy) can be configured with various distribution algorithms like round-robin or least connections. These algorithms determine how incoming requests are assigned to backend servers, ensuring optimal resource utilization.
Active-Active vs. Active-Passive Setup: The setup enables an Active-Active configuration, allowing both the load balancer and backend servers to actively process requests simultaneously. This configuration improves resource utilization and scalability.
Primary-Replica (Master-Slave) Database Cluster: The database is implemented as a Primary-Replica cluster, where the primary node handles write operations and synchronizes changes to the replica nodes. Replica nodes primarily serve read operations, improving availability, scalability, and fault tolerance.
Primary Node vs. Replica Node: The primary node handles write operations, ensuring data consistency. Replica nodes replicate data from the primary node and primarily handle read operations, providing scalability and serving as backups in case the primary node fails.
Issues with the Infrastructure:

Single Point of Failure (SPOF): The infrastructure lacks redundancy, which could result in downtime or reduced availability if any critical component fails. Redundancy should be added to mitigate this risk.
Security Issues: The infrastructure lacks a firewall and HTTPS, exposing it to potential unauthorized access and leaving communications unencrypted. Implementing a firewall and enabling HTTPS is necessary for enhanced security.
No Monitoring: The infrastructure lacks monitoring, making it challenging to track health, performance, and availability. Monitoring is crucial for detecting issues and ensuring timely troubleshooting and maintenance.





task 02

The task is to design a secure and monitored three-server web infrastructure on a whiteboard for hosting the website www.foobar.com. The requirements include adding three firewalls, implementing SSL encryption for HTTPS traffic, and incorporating three monitoring clients.

Specifics of the Infrastructure:

Firewalls: Added for enhanced security by controlling network traffic and preventing unauthorized access.
SSL Certificate for HTTPS: Implemented to serve encrypted traffic, ensuring secure communication between the website and clients.
Monitoring Clients: Included to monitor the infrastructure's health, performance, and availability by collecting data from various components.
Key Points:

Firewalls provide security by filtering traffic.
HTTPS ensures encrypted communication for data protection.
Monitoring clients collect data for real-time tracking and issue detection.
Monitoring tools utilize agents, APIs, or data collectors for data collection.
To monitor web server QPS, relevant metrics are collected, such as request rates and response times.
Issues with the Infrastructure:

Terminating SSL at the load balancer level can introduce security risks due to transmitting decrypted traffic internally.
Having only one MySQL server capable of accepting writes creates a single point of failure.
Servers with identical components increase the risk of widespread failure if a vulnerability affects one component.


