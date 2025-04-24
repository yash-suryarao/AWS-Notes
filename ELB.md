Elastic Load Balancer :

      Elastic Load Balancing automatically distributes your incoming traffic across multiple targets, such 
      as EC2 instances, containers, and IP addresses, in one or more Availability Zones.

Load balancer benefits
      
      - A load balancer distributes workloads across multiple compute resources, such as virtual servers. 
        Using a load balancer increases the availability and fault tolerance of your applications.
      - You can add and remove compute resources from your load balancer as your needs change, without 
        disrupting the overall flow of requests to your applications.
      - You can configure health checks, which monitor the health of the compute resources, so that the 
        load balancer sends requests only to the healthy ones. You can also offload the work of encryption 
        and decryption to your load balancer so that your compute resources can focus on their main work.

Key Concepts

1. Load Balancer
   
         - Distributes incoming traffic across multiple targets.
         - Enhances fault tolerance and availability.

3. Target
   
         - Resources that receive traffic from the load balancer, such as EC2 instances or containers.
         - Registered with the load balancer in target groups.

5. Target Group
   
         - A logical grouping of targets.
         - Health checks are performed on targets within the group.

7. Listeners
   
         - Process that checks for connection requests from clients.
         - Configured with a protocol and port number

Types of AWS ELB

AWS provides four types of load balancers, each catering to different use cases and requirements:

      1. Application Load Balancer (ALB)
      2. Network Load Balancer (NLB)
      3. Classic Load Balancer (CLB)
      4. Gateway Load Balancer (GWLB)

1. Application Load Balancer (ALB)

         - Use Case: Ideal for HTTP/HTTPS traffic and application layer (Layer 7) routing.
         - Features:
           - Path-based and host-based routing.
           - Advanced request routing (e.g., URL-based routing).
           - Integration with AWS WAF for web application security.
           - Support for WebSocket connections.
           - SSL/TLS termination.
         - Target Types: EC2 instances, ECS tasks, IP addresses, Lambda functions.
         - Health Checks: HTTP/HTTPS health checks.


 2. Network Load Balancer (NLB)

         - Use Case: Designed for ultra-high performance, low latency,and handling TCP/UDP traffic(Layer 4).
         - Features:
           - Can handle millions of requests per second.
           - Provides static IP addresses.
           - Supports Elastic IP addresses.
           - Suitable for applications requiring extreme performance and low latency.
           - Preserves the source IP of the client.
         - Target Types: EC2 instances, IP addresses, on-premises servers.
         - Health Checks: TCP/HTTP/HTTPS health checks.


3. Classic Load Balancer (CLB)

         - Use Case: Used for both HTTP/HTTPS and TCP applications (Layer 4 and Layer 7).
         - Features:
           - Basic load balancing features for legacy applications.
           - Supports sticky sessions.
           - SSL termination and SSL certificate management.
           - Ideal for simple load balancing needs or legacy applications.
         - Target Types: EC2 instances.
         - Health Checks: TCP/HTTP/HTTPS health checks.

4. Gateway Load Balancer (GWLB)

         - Use Case: Ideal for third-party virtual appliances, such as firewalls, intrusion detection and 
                     prevention systems, deep packet inspection systems, and other network security and 
                     monitoring appliances.
         - Features:
           - Simplifies deployment, scalability, and management of virtual appliances.
           - Operates at Layer 3 (network layer), routing traffic to the target appliances.
           - Provides high availability and auto-scaling of virtual appliances.
           - Integration with AWS Gateway Load Balancer Endpoints (GWLBE) for seamless routing.
         - Target Types: EC2 instances acting as virtual appliances.
         - Health Checks: TCP/HTTP/HTTPS health checks.


