EC2 : Elastic Compute Cloud 

    Amazon Elastic Compute Cloud (Amazon EC2) provides scalable, on-demand virtual servers (called "instances") in the cloud, letting you rent computing power (CPU, memory, storage, networking) to run applications without buying physical hardware

Features of Amazon EC2 /Key Concepts :

    Instances :
    Virtual servers that run applications.
    Configured with specific amounts of CPU, memory, and storage.
    Can be launched using predefined Amazon Machine Images (AMIs).
    
    Amazon Machine Images (AMIs):
    Preconfigured Templates that contain the software configuration (operating system, application server, 
    and applications) required to launch an instance.
    Available in public, AWS Marketplace, or created as custom AMIs.
    
    Instance types:
    Various configurations of CPU, memory, storage, networking capacity, and graphics hardware for your 
    instances.
    Categorized based on use case: General Purpose, Compute Optimized, Memory Optimized, Storage 
     Optimized, and Accelerated Computing.
    
    Key pairs:
    Secure login information for your instances. 
    AWS stores the public key and you store the private key in a secure place.
    
    Instance store volumes:
    Temporary storage that is physically attached to the host instance.
    Storage volumes for temporary data that is deleted when you stop, hibernate, or terminate your 
    instance.
    
    Amazon EBS volumes:
    Persistent storage volumes for your data using Amazon Elastic Block Store (Amazon EBS).
    Types include General Purpose SSD (gp2, gp3), Provisioned IOPS SSD (io1, io2), Throughput Optimized 
    HDD (st1), and Cold HDD (sc1).
    
    Regions and Zones:
    Multiple physical locations for your resources, such as instances and Amazon EBS volumes.
    
    Security groups:
    A virtual firewall that allows you to specify the protocols, ports, and source IP ranges that can 
    reach your instances, and the destination IP ranges to which your instances can connect.
    
    Elastic IP addresses:
    Static IPv4 addresses for dynamic cloud computing.
    
    Tags:
    Metadata that you can create and assign to your Amazon EC2 resources.
    
    Virtual private clouds (VPCs):
    Virtual networks you can create that are logically isolated from the rest of the AWS Cloud. You can 
    optionally connect these virtual networks to your own network.


 EC2 Instance Types :
When choosing an instance type, consider the following factors:

    - Workload Requirements: Match the instance type to the compute, memory, storage, and networking 
                              requirements of your application.
    - Cost Efficiency: Balance performance needs with budget constraints by selecting the most cost- 
                       effective instance type for your workload.
    - Scalability: Consider the scalability needs of your application and choose instance types that can 
                   be easily scaled horizontally (adding more instances) or vertically (switching to 
                   larger instance types).


AWS EC2 instances are broadly classified into several families, each optimized for different workloads:

 Instance Types: 
 
            1. General Purpose Instances
                series T,M 
            2. Compute Optimized Instances
                Series C               
            3. Memory Optimized Instances
                Series R,X,Z 
            4. Accelerated Computing Instances
                Series P,N,G 
            5. Storage optimized Instances
                Series I,D 
            6. HPC(High Performance Computing) Optimized 
                Series H
  

1. General Purpose Instances
   
       General Purpose instances provide a balanced mix of compute, memory, and networking resources, making them suitable for a variety of workloads.
       
       - Use Cases: Web servers, development environments, small to medium databases, application servers.
       - Instance Families:
         - T4g: Cost-effective instances with burstable performance, powered by AWS Graviton2 processors.
         - T3/T3a: Burstable performance instances with the ability to sustain high CPU performance for 
                    extended periods.
         - M6g: General purpose instances powered by AWS Graviton2 processors.
         - M5/M5a/M5n: Latest generation general purpose instances with a balance of compute, memory, and 
                       networking.
         - M4: Previous generation general purpose instances.
       
       Example Configuration for M5 Instance:
       - m5.large: 2 vCPUs, 8 GiB memory.
       - m5.xlarge: 4 vCPUs, 16 GiB memory.
       - m5.2xlarge: 8 vCPUs, 32 GiB memory.

3. Compute Optimized Instances

       Compute Optimized instances are ideal for compute-bound applications that benefit from high- 
       performance processors.
       
       - Use Cases: High-performance web servers, scientific modeling, batch processing, machine learning 
                     inference.
       - Instance Families:
         - C6g: Compute optimized instances powered by AWS Graviton2 processors.
         - C5/C5a/C5n: Latest generation compute optimized instances with high performance and cost efficiency.
         - C4: Previous generation compute optimized instances.

        Example Configuration for C5 Instance:
        - c5.large: 2 vCPUs, 4 GiB memory.
        - c5.xlarge: 4 vCPUs, 8 GiB memory.
        - c5.2xlarge: 8 vCPUs, 16 GiB memory.

4. Memory Optimized Instances
   
       Memory Optimized instances are designed to deliver fast performance for workloads that process 
       large datasets in memory.
       
       - Use Cases: High-performance databases, in-memory caching, big data analytics, real-time 
                    processing.
       - Instance Families:
         - R6g: Memory optimized instances powered by AWS Graviton2 processors.
         - R5/R5a/R5n: Latest generation memory optimized instances with a high ratio of memory to vCPUs.
         - X1/X1e: Instances with large memory footprints suitable for SAP HANA and other memory-intensive 
                    applications.
         - High Memory Instances: Instances with up to 24 TB of memory for large-scale, in-memory 
                                  databases like SAP HANA.
         - z1d: High frequency instances with both high compute and memory resources.
       
       Example Configuration for R5 Instance:
       - r5.large: 2 vCPUs, 16 GiB memory.
       - r5.xlarge: 4 vCPUs, 32 GiB memory.
       - r5.2xlarge: 8 vCPUs, 64 GiB memory.

 5. Storage Optimized Instances

        Storage Optimized instances are designed for workloads that require high, sequential read and 
        write access to large datasets on local storage.
        
        - Use Cases: NoSQL databases, data warehousing, distributed file systems.
        - Instance Families:
          - I3/I3en: High I/O instances with NVMe SSD-based instance storage.
          - D2: Dense storage instances with HDD-based storage for data-intensive workloads.
          - H1: Instances with high disk throughput and large HDDs for big data and data warehousing 
               applications.
        
        Example Configuration for I3 Instance:
        - i3.large: 2 vCPUs, 15.25 GiB memory, 1 x 475 GB NVMe SSD.
        - i3.xlarge: 4 vCPUs, 30.5 GiB memory, 1 x 950 GB NVMe SSD.
        - i3.2xlarge: 8 vCPUs, 61 GiB memory, 1 x 1.9 TB NVMe SSD.

6. Accelerated Computing Instances
   
        Accelerated Computing instances use hardware accelerators or co-processors to perform functions 
         such as floating-point number calculations, graphics processing, or data pattern matching more 
         efficiently than is possible in software running on general-purpose CPUs.
       
       - Use Cases: Machine learning, deep learning, computational fluid dynamics, speech recognition, 
                    autonomous driving, high-performance computing (HPC).
       - Instance Families:
         - P4/P3: GPU instances optimized for machine learning and HPC.
         - Inf1: Instances with AWS Inferentia chips for machine learning inference.
         - G4ad/G4dn: GPU instances optimized for graphics-intensive applications and ML inference.
         - F1: FPGA instances for custom hardware acceleration.
       
       Example Configuration for P3 Instance:
       - p3.2xlarge: 8 vCPUs, 61 GiB memory, 1 x NVIDIA V100 GPU.
       - p3.8xlarge: 32 vCPUs, 244 GiB memory, 4 x NVIDIA V100 GPUs.
       - p3.16xlarge: 64 vCPUs, 488 GiB memory, 8 x NVIDIA V100 GPUs.

Reference link :https://aws.amazon.com/ec2/instance-types/

AWS Pricing Options :

AWS offers a variety of pricing models to suit different business needs and use cases. 

1. On-Demand Instances
   
       - On-Demand Instances let you pay for compute or database capacity by the hour or second (minimum 
          of 60 seconds) with no long-term commitments or upfront payments.
       - This pricing model is ideal for users who want the flexibility to change instance types or 
           configurations frequently, and for applications with unpredictable workloads.
       
       Use Cases:
       - Applications with short-term, spiky, or unpredictable workloads.
       - Development and test environments.
       - Applications being tested for the first time.
       
       Pros:
       - No upfront costs.
       - Pay for what you use.
       - Easy to start and stop instances as needed.
       
       Cons:
       - Higher cost compared to reserved instances for sustained workloads.

2. Reserved Instances
   
       - Reserved Instances (RIs) offer significant savings (up to 75%) compared to On-Demand pricing by 
         committing to use AWS for a 1- or 3-year term.
       - RIs provide a billing discount and are available for various instance types.
       
       Types:
       - Standard RIs: Offer the most significant discount and are best suited for steady-state usage.
       - Convertible RIs: Allow you to change the instance family, operating system, and tenancy during 
        the term. Offer a lower discount than Standard RIs.
       - Scheduled RIs: Enable you to reserve capacity for specific time periods, recurring daily, weekly, 
        or monthly, with a 1-year term.
       
       Use Cases:
       - Applications with predictable usage patterns.
       - Long-term workloads.
       
       Pros:
       - Significant cost savings.
       - Reserved capacity in specific availability zones.
       
       Cons:
       - Requires commitment to a specific region and instance type.
       - Less flexibility compared to On-Demand instances.

3. Savings Plans
   
       - Savings Plans offer a flexible pricing model that provides significant savings on AWS usage (up 
         to 72%) in exchange for a commitment to a consistent amount of usage (measured in $/hour) for a 
         1- or 3-year term.
       
       Types:
       - Compute Savings Plans: Provide the most flexibility and apply automatically to any EC2 instance 
        usage, regardless of instance family, region, OS, or tenancy, and also apply to AWS Fargate and 
        Lambda usage.
       - EC2 Instance Savings Plans: Provide the highest discount but are less flexible. They apply to 
         specific EC2 instance families within a region.
       
       Use Cases:
       - Users who need flexibility across different instance types and regions.
       - Applications that run continuously.
       
       Pros:
       - Flexibility in usage.
       - Significant savings similar to Reserved Instances.
       
       Cons:
       - Commitment required.
       - Lower savings compared to Standard RIs for specific instance types.

4. Spot Instances
   
       - Spot Instances allow you to bid for spare AWS capacity at significantly reduced prices (up to 90% 
         off On-Demand rates).
       - AWS can reclaim Spot Instances with a two-minute warning when it needs the capacity back.
       
       Use Cases:
       - Fault-tolerant and flexible applications.
       - Batch processing, big data analytics, and CI/CD workloads.
       - Stateless web servers.
       
       Pros:
       - Very low cost.
       - Suitable for flexible workloads.
       
       Cons:
       - Instances can be terminated at any time.
       - Not suitable for critical or time-sensitive workloads.

5. Dedicated Hosts and Instances

       Overview:
       - Dedicated Hosts: Physical servers dedicated to your use. They help you meet compliance 
         requirements and reduce costs by using your existing server-bound software licenses.
       - Dedicated Instances: Instances that run on hardware dedicated to a single customer.
       
       Use Cases:
       - Applications with specific compliance requirements.
       - Workloads that require isolation from other customers.
       
       Pros:
       - Dedicated hardware.
       - Enhanced control and compliance.
       
       Cons:
       - Higher cost compared to shared instances.
       - Less flexibility.

Reference Link :https://aws.amazon.com/ec2/pricing/

