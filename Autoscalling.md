AWS AUTO SCALING :

          AWS Auto Scaling is a service that automatically adjusts the capacity of your resources to 
          maintain steady, predictable performance at the lowest possible cost. 
          It scales your Amazon EC2 instances and other AWS resources in response to changing demand
          It supports scaling for several types of resources, including EC2 instances, ECS tasks, DynamoDB 
          tables, and Aurora replicas.

*Benefits of AWS Auto Scaling* :

          Cost Efficiency: Automatically adjusts capacity to meet current demand, helping to avoid over- 
                            provisioning and reducing costs.
          High Availability: Ensures applications remain available by distributing instances across 
                             multiple Availability Zones.
          Performance Optimization: Maintains performance by adjusting capacity based on actual traffic 
                                    patterns.
          Fault Tolerance: Automatically replaces unhealthy instances to maintain the desired capacity.

*Use Cases*:

          Web Applications: Automatically scale web server instances based on traffic patterns.
          Batch Processing: Scale instances based on the number of jobs in a queue.
          Microservices: Ensure each microservice scales independently based on its load.
          E-commerce Platforms: Handle seasonal spikes in traffic by automatically adjusting resources.

Horizontal Scaling and Vertical Scaling are two strategies for adjusting the capacity of your resources.

1.Horizontal Scaling (Scale Out/In)

          Definition:    Adding or removing instances (servers) to handle an increase or decrease in load.
          Advantages:   Improves redundancy and fault tolerance by distributing the load across multiple 
                        instances. It's easier to scale beyond the limits of a single instance.
          Auto Scaling: AWS Auto Scaling primarily supports horizontal scaling by adjusting the number 
                        of instances in an Auto Scaling group.
          Example:      Increasing the number of EC2 instances from 2 to 10 during peak traffic and the 
                         reducing them  back to 2 when traffic decreases.

2.Vertical Scaling (Scale Up/Down)

          Definition: Increasing or decreasing the size (capacity) of a single instance (e.g., adding more 
                      CPU, memory, or storage).
          Advantages: Simpler to manage because it involves fewer instances. However, it's limited by the 
                      maximum capacity of the instance type.
          AWS Support: AWS allows vertical scaling through instance resizing, but this is not handled by 
                       Auto Scaling. Instead, you would stop the instance, change its instance type, and 
                       restart it.
          Example:    Upgrading an instance from t2.micro to t2.large to handle more load.


*Key Concepts* :

Auto Scaling Group (ASG):

          A logical grouping of EC2 instances.
          Ensures you have the correct number of instances available to handle the load of application.
          Defined by minimum, maximum, and desired capacity.

Scaling Policies:

          Define how the Auto Scaling group should respond to changes in demand.
          Types include target tracking, step scaling, and simple scaling.

Launch Configuration/Launch Template:

          Define the instance configuration for the Auto Scaling group.
          Launch Templates are recommended over Launch Configurations due to additional features and 
          flexibility.

Health Checks:

          Determine the health status of instances within the ASG.
          Can be EC2 status checks or custom health checks.

Lifecycle Hooks:

          Allow you to perform custom actions when instances launch or terminate.
          Useful for initializing instances with custom software or scripts.



*Types of Scaling*

1.Dynamic Scaling

Adjusts the number of instances based on real-time changes in demand.

There are three types of dynamic scaling policies:

          Target Tracking Scaling:
          
          Adjusts the number of instances to maintain a target metric, such as average CPU utilization.
          Example: Keep average CPU utilization at 50%.
          
          Step Scaling:
          Adjusts the number of instances in steps, based on the size of the alarm breach.
          Example: Add more instances if the load increases significantly.
          
          Simple Scaling:
          Adds or removes instances based on a single scaling adjustment.
          Example: Add one instance when CPU utilization exceeds 70%.

2. Scheduled Scaling
   
          Scales the number of instances based on a predefined schedule.
          Useful for predictable workload patterns.
          Example: scaling up every weekday morning at 9 AM and scaling down at 5 PM).

4. Predictive Scaling
   
          Uses machine learning to forecast future traffic and automatically provision the right number of 
          instances ahead of time.
          Integrates with CloudWatch metrics and historical data to predict demand.
          Example: Scale out before a predicted traffic spike.
          

Steps to Implement Auto Scaling :

          Step 1: Create a Launch Template/Configuration
          Define the instance configuration, including the AMI ID, instance type, key pair, security 
          groups, and other settings.
          
          Step 2: Create an Auto Scaling Group
          Specify the minimum, maximum, and desired capacity, and attach the Launch Template.
          
          Step 3: Set Up Scaling Policies
          Define dynamic or scheduled scaling policies based on CloudWatch alarms or specific schedules.
          
          Step 4: Create CloudWatch Alarms
          Create CloudWatch alarms to trigger scaling policies based on metrics like CPU utilization.
          
          Step 5: Monitoring and Health Checks
          Configure health checks and set up monitoring to ensure instances are functioning correctly.
