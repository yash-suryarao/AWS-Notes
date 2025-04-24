 Amazon EFS

Amazon Elastic File System (EFS) is a scalable, fully-managed file storage service for use with AWS Cloud services and on-premises resources. 
It is designed to provide scalable file storage that can grow and shrink automatically as you add and remove files, with no need for management or provisioning.

Key Features

- Scalability: Automatically scales up or down based on demand.
- Performance: Offers two performance modes (General Purpose and Max I/O) and two throughput modes (Bursting and Provisioned).
- Availability and Durability: Provides high availability and durability.
- Security: Supports encryption of data at rest and in transit.
- Access Control: Integrated with AWS IAM and security groups for controlling access.

 Use Cases

- Web serving and content management
- Application development and testing
- Media processing workflows
- Big data and analytics
- Backup and disaster recovery


Steps to Create an EFS

1. Create EFS File System
   - Navigate to the EFS console.
   - Click "Create file system".
   - Configure settings such as VPC, availability zones, and performance modes.
   - Review and create the file system.

2. Configure Security Groups
   - Ensure the EC2 instances and EFS have security groups that allow NFS traffic (port 2049).

3. Mount Targets
   - Create mount targets for the EFS in each availability zone you want to use.

Using EFS with EC2

Objective

Set up an EFS file system and mount it on two EC2 instances in the same VPC.

Lab Steps

1. Launch two EC2 instances in the same VPC and subnet. Use Amazon Linux 2 AMI.

2. create an EFS File System

3. Install NFS Client on EC2 Instances
   - SSH into each EC2 instance.
   - Install the NFS client using the following commands:
   
     sudo yum -y update
     sudo yum -y install nfs-utils

4. Mount the EFS File System
   - Create a directory to mount the EFS:
     sudo mkdir /mnt/efs

   - Mount the EFS file system:
     sudo mount -t nfs4 -o nfsvers=4.1 <EFS_DNS_Name>:/ /mnt/efs
 
   - Verify the mount:
     df -h
    

5. Test the File System
   - Create a test file:
     echo "Hello EFS" | sudo tee /mnt/efs/hello.txt
    
   - Verify the file is accessible from both EC2 instances:
      cat /mnt/efs/hello.txt
     

 Cleanup

- Unmount the EFS file system:
  sudo umount /mnt/efs
 
- Terminate the EC2 instances.
- Delete the EFS file system from the console.

