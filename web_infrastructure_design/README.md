# Web infrastructure design



#### task 0   Simple web stack

```
A lot of websites are powered by simple web infrastructure, a lot of time it is composed of a single server with a LAMP stack.

On a whiteboard, design a one server web infrastructure that hosts the website that is reachable via www.foobar.com. Start your explanation by having a user wanting to access your website.

Requirements:

You must use:
1 server
1 web server (Nginx)
1 application server
1 application files (your code base)
1 database (MySQL)
1 domain name foobar.com configured with a www record that points to your server IP 8.8.8.8
You must be able to explain some specifics about this infrastructure:
What is a server
What is the role of the domain name
What type of DNS record www is in www.foobar.com
What is the role of the web server
What is the role of the application server
What is the role of the database
What is the server using to communicate with the computer of the user requesting the website
You must be able to explain what the issues are with this infrastructure:
SPOF
Downtime when maintenance needed (like deploying new code web server needs to be restarted)
Cannot scale if too much incoming traffic
```

The domain name www.foobar.com that the user enters in his browser to access the website is displayed at the top.

The DNS request is then sent to the DNS server that resolves the domain name to the server's IP address.

The web server (Nginx) receives the HTTP request and handles the static requests directly, returning the HTML files, CSS, images, etc., to the user.

Dynamic requests are sent to the application server, which is responsible for processing the application logic and generating dynamic responses.

The application server can interact with the database (MySQL) to obtain or store data needed for the web application.

Finally, the response is sent back to the web server and then to the user, who views the website in his browser.

![imagen web](https://github.com/binbashz/holbertonschool-system_engineering-devops/assets/124454895/9360137f-b512-44eb-9915-161b91f6ddf0)




### task 01  Distributed web infrastructure

```
On a whiteboard, design a three server web infrastructure that hosts the website www.foobar.com.

Requirements:

You must add:
2 servers
1 web server (Nginx)
1 application server
1 load-balancer (HAproxy)
1 set of application files (your code base)
1 database (MySQL)
You must be able to explain some specifics about this infrastructure:
For every additional element, why you are adding it
What distribution algorithm your load balancer is configured with and how it works
Is your load-balancer enabling an Active-Active or Active-Passive setup, explain the difference between both
How a database Primary-Replica (Master-Slave) cluster works
What is the difference between the Primary node and the Replica node in regard to the application
You must be able to explain what the issues are with this infrastructure:
Where are SPOF
Security issues (no firewall, no HTTPS)
No monitoring
```

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


```
if the load balancer is configured to have an active-active or active-passive setup
the load balancer is stilla sigle pint of failure
traffic is unecrypted
no monitoring
```
![img 2](https://github.com/binbashz/holbertonschool-system_engineering-devops/assets/124454895/d1b81be8-3b8e-4dc8-964b-4f91bf84b5bc)




### task 02   Secured and monitored web infrastructure

```
On a whiteboard, design a three server web infrastructure that hosts the website www.foobar.com, it must be secured, serve encrypted traffic, and be monitored.

Requirements:

You must add:
3 firewalls
1 SSL certificate to serve www.foobar.com over HTTPS
3 monitoring clients (data collector for Sumologic or other monitoring services)
You must be able to explain some specifics about this infrastructure:
For every additional element, why you are adding it
What are firewalls for
Why is the traffic served over HTTPS
What monitoring is used for
How the monitoring tool is collecting data
Explain what to do if you want to monitor your web server QPS
You must be able to explain what the issues are with this infrastructure:
Why terminating SSL at the load balancer level is an issue
Why having only one MySQL server capable of accepting writes is an issue
Why having servers with all the same components (database, web server and application server) might be a problem
```

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

```
Firewall filters network traffic in and out machine
HTTPS is setuo so that if someone intercepts the traffic , it cannot be read
monitoring can be used to check something is broken or slow
the monitoring setup is composed of a client collecting data and sending it to the monitoring system
Configure monitoring to:

collect web server data
have an alert triggered if QPS is getting out of control

Terminating SSL at the load balancer level is an issue because the traffic between the load balancer and the web servers is unencrypted
MySQL server capable of accepting writes is an issue because if the master goes down, the application cannot write to the database anymore

Having servers with all the same components (database, web server and application server) might be a problem because their consumption will not grow the same way between each of them (we might want to have more database servers than application servers for instance).

Having servers with all the same components (database, web server and application server) might be a problem because when there is maintenance performed on a server for a specific component, it will affect other components that are on it
Load-balancer is a SPOF
```
![IMG3](https://github.com/binbashz/holbertonschool-system_engineering-devops/assets/124454895/de2a0f8b-3733-4c1c-a0e9-b2d8119c6155)


### task 03 Scale up
```
## Application server vs web server
Requirements:

You must add:
1 server
1 load-balancer (HAproxy) configured as cluster with the other one
Split components (web server, application server, database) with their own server
You must be able to explain some specifics about this infrastructure:
For every additional element, why you are adding it
```


##### Application Server vs. Web Server:

Web Server: A web server is responsible for handling HTTP requests from clients (such as web browsers) and delivering static content, such as HTML, CSS, and images, to the clients. It serves as the intermediary between the client and the application server, handling the initial processing and routing of requests.
Application Server: An application server executes the application's business logic and generates dynamic content. It processes requests received from the web server, interacts with databases or other services, and generates responses to be sent back to the web server for delivery to the client.
Additional Elements and Their Significance:

Server: The server is added to provide the hardware and resources necessary to host the infrastructure components. It serves as the foundation for running the web server, application server, and database.
Load Balancer (HAproxy) Configured as a Cluster: The load balancer is added to distribute incoming traffic evenly across multiple servers to improve performance, scalability, and fault tolerance. Configuring it as a cluster ensures redundancy and high availability.
Splitting Components Across Separate Servers: Separating the components onto their own servers provides several benefits, including:
Isolation: Isolating components enhances security and reduces the impact of failures or performance issues in one component on the others.
Scalability: Each component can be scaled independently based on its specific requirements. For example, if the application server requires more resources, only that server needs to be scaled.
Modularity: Splitting components allows for easier maintenance, updates, and troubleshooting, as changes made to one component are less likely to impact others.

---------------------------------------------------------------------------------------------------------------------------------------



 #### Also keep in mind when we look at the whiteboard diagram
```
the server is located in a data center
the server can be physical or virtual
the server run an OS
the web server's role is to server web pages (static content)
an application server's role is to compute dynamic content
the data base's role is to store application data
is an a record because its resolves to an IP adress
the server is an single point to faiulre because nothing is redundant
the website would be temporarily down when code is deployed and the web server needs to be restarted
this infrastructure cannot scale and will not be able to handle traffic that would exceed the server capacity
```
