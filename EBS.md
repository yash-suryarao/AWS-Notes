 ELASTIC BLOCK STORE (EBS)

There are two types of block store devices are available for EC2. 

1. Instances Store Backed EC2:
   
        • Basically the virtual hard drive on the host allocated to this EC2 instance.
        • Limit to 10GB per device 
        • Ephemeral storage (non-persistent storage) 
        • The EC2 instance can’t be stopped, can only be rebooted or terminated. 
            Terminate will delete data. 

3. Elastic Block Store (persistent, network attached virtual drive)
   
            - EBS volume behaves like RAW, unformatted, external block storage devices that you 
            can attached to your EC2 instance. 
            - EBS volumes are block storage devices suitable for database style data that requires 
            frequent reads and writes. 
            - EBS volumes are attached to your EC2 instances through the AWS network, like virtual 
            hard drive. 
            - Both EBS volumes and EC2 instances must be in the same AZ. 

EBS Volume Types: 

     1. SSD backed volume 
     2. HDD backed volume 
     3. Magnetic standard 


General Purpose SSD (gp2 and gp3)
Reference link :https://docs.aws.amazon.com/ebs/latest/userguide/ebs-volume-types.html
gp2 Volumes:
   
        - Key Characteristics:
          - Baseline Performance: 3 IOPS per GB, up to 16,000 IOPS.
          - Burst Performance: Smaller volumes can burst up to 3,000 IOPS based on burst credits.
          - Throughput: Up to 250 MB/s.
        - Use Cases: 
          - Boot volumes for EC2 instances.
          - Small to medium-sized databases.
          - Development and test environments.
          - General-purpose workloads that need a balance of price and performance.

gp3 Volumes:

    - Key Characteristics:
      - IOPS: Provision up to 16,000 IOPS.
      - Throughput: Provision up to 1,000 MB/s.
      - Cost: Lower cost per GB compared to gp2 and allows independent provisioning of IOPS and throughput.
    - Use Cases:
      - General-purpose workloads that require higher performance than gp2.
      - Large databases.
      - Enterprise applications with higher performance requirements.
      - Applications needing predictable performance at a lower cost.

 Provisioned IOPS SSD (io1 and io2)
   
   io1 Volumes:
    
        - Key Characteristics:
        - IOPS: Up to 64,000 IOPS for Nitro-based instances and up to 32,000 IOPS for other instances.
        - Throughput: Up to 1,000 MB/s.
       - Use Cases:
        - High-performance relational databases (e.g., MySQL, PostgreSQL).
        - NoSQL databases (e.g., Cassandra, MongoDB).
        - Large-scale transactional systems.
        - Applications requiring sustained IOPS performance.

io2 Volumes:

    - Key Characteristics:
      - IOPS: Up to 64,000 IOPS.
      - Throughput: Up to 1,000 MB/s.
      - Durability: 99.999% durability, making it 100 times more durable than io1.
    - Use Cases:
      - Mission-critical databases (e.g., Oracle, SAP HANA).
      - Enterprise applications with stringent performance and durability requirements.
      - Applications needing highly consistent IOPS performance.
      - Transactional systems requiring high availability.

Throughput Optimized HDD (st1)
 
       - Key Characteristics:
       - Throughput: 40 MB/s per TB, up to 500 MB/s.
       - Burst Throughput: Up to 250 MB/s per TB.
       - Cost: Lower cost per GB compared to SSDs.
       - Use Cases:
        - Big data analytics.
        - Data warehousing.
        - Log processing.
        - Streaming workloads.
        - Applications with large, sequential data access patterns.

Cold HDD (sc1)
   
       - Key Characteristics:
        - Throughput: 12 MB/s per TB, up to 250 MB/s.
        - Burst Throughput: Up to 80 MB/s per TB.
        - Cost: Lowest cost per GB among EBS volumes.
        - Use Cases:
        - Infrequently accessed data.
        - Archival storage.
        - Backup solutions.
        - Data that is rarely updated but needs to be retained.

 Magnetic Volumes (Standard)

        - Key Characteristics:
          - IOPS: 40-200 IOPS.
          - Throughput: Performance varies.
        - Cost: Low-cost storage option.
        - Use Cases:
          - Legacy systems.
          - Low-cost storage needs where performance is not critical.
          - Archival data.
          - Scenarios with minimal performance requirements.


 IOPS gives us a measure of how many read and write operations a storage device can handle in a single 
  second. 
 Throughput, often measured in megabytes per second, tells us about the actual data transfer rate.

 EBS Volume Management :

Terminology

    - Partition: A logical division of a storage device, such as an EBS volume, that can be formatted with 
      a file system and mounted.
    - Mount Point: A directory in the file system where a partition or volume is attached for access.
    - File System: A method for organizing and storing files on a partition (e.g., ext4, xfs).
    - UUID (Universally Unique Identifier): A unique identifier assigned to storage devices and 
      partitions, used for consistent mounting.
    - `/etc/fstab`: A configuration file in Unix-like operating systems that defines how disk partitions 
      and other file systems should be mounted.


After attaching an EBS volume to an EC2 instance, you typically need to create a file system, create partitions, mount the partitions, and ensure they mount automatically on reboot. Here are detailed notes on these processes.

1. Creating Partitions

              1. Attach the EBS Volume:
                 - Attach your EBS volume to your EC2 instance using the AWS Management Console, AWS CLI.
                 - Note the device name (e.g., `/dev/xvdf`).
              
              2. Identify the Device:
               
                 lsblk
                 - This command lists all available block devices. Identify your newly attached EBS volume.
              
              3. Create Partitions using `fdisk`:
               
                 sudo fdisk /dev/xvdf
               
                 - Follow the steps:
                   - Press `n` to create a new partition.
                   - Select `p` for primary partition.
                   - Choose the partition number (usually `1` for the first partition).
                   - Accept the default first sector.
                   - Accept the default last sector or specify a size.
                   - Press `w` to write the partition table and exit.
              
              4. Verify the Partition:
              
                 lsblk
                 - The new partition should appear as `/dev/xvdf1`.


2. Creating a File System

                  1. Create a File System:
                     - to create an ext4 file system:
                       sudo mkfs.ext4 /dev/xvdf1
                      
                     - Other file systems:
                       - XFS: `sudo mkfs.xfs /dev/xvdf1`
                       - EXT3: `sudo mkfs.ext3 /dev/xvdf1`

3. Mounting Partitions

                  1. Create a Mount Point:
                     sudo mkdir /mnt/mydata
                  
                  
                  2. Mount the Partition:
                     sudo mount /dev/xvdf1 /mnt/mydata
                  
                  3. Verify the Mount:
                     df -h
                     - This command shows the mounted file systems. Verify that `/dev/xvdf1` is mounted to `/mnt/mydata`.

4. Permanent Mount Configuration
   
        To ensure the partition mounts automatically after a reboot, update the `/etc/fstab` file.

                  1. Get the UUID of the Partition:
                   
                     sudo blkid /dev/xvdf1
                     - Copy the UUID from the output.
                  
                  2. Edit `/etc/fstab`:
                     sudo nano /etc/fstab
                  - Add an entry for the new partition. Use the UUID from the previous step. For example:
                    
                       UUID=your-uuid-here /mnt/mydata ext4 defaults,nofail 0 2
                      
                  - Replace `your-uuid-here` with the actual UUID and adjust the file system type if 
                        necessary.


 
EBS Snapshot of Root Volume and Non-root Volume: 

        ➢ EBS snapshots are point-in-time images/copies of your EBS volume. 
        ➢ Any data written to the volume after the snapshot process is initiated, will not be 
        included in the resulting snapshot (but will be included in future incremental update.) 
        ➢ Per AWS account up to 5000 EBS volumes can be created. 
        ➢ Per account up to 10,000 EBS snapshots can be created. 
        ➢ EBS snapshots are stored on S3, however you cannot access them directly. You can 
        only access them through EC2 APIs. 
        ➢ While EBS volumes are AZ specific, snapshots are region specific. 
        ➢ Any AZ in region can use snapshot to create EBS volume. 
        ➢ To migrate an EBS from one AZ to another, create a snapshot (region specific) and 
        create an EBS volume from the Snapshot in the intended AZ. 
        ➢ You can create a snapshot to an EBS volume of the same or larger size than the original 
        volumes size from which the snapshot was initially created. 
        ➢ You can take a snapshot of a non-root EBS volume while the volumes is in use on a 
        running EC2 instance. 


Incremental Snapshot: 

        ➢ EBS snapshots are stored incrementally. 
        ➢ For low cost storage on S3 and a guarantee to be able to able fully restore data from the 
        snapshot. 
        ➢ What you need is a single snapshot then further snapshot will only carry the changed 
        blocks (incremental updates). 
        ➢ Therefore you do not need to have multiple full/complete copies of the snapshot. 
        ➢ You are charged for: 
        • Data transferred to S3 from your EBS volume you are taking snapshot. 
        • Snapshot stored in S3. 
        • First snapshot is a clone, subsequent snapshots are incremental. 
        • Deleting snapshot will only remove data exclusive to that snapshot. 

