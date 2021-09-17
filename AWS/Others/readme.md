# Others

1. Failure in processing a message from SQS FIFO queue will result in blocking 
2. With SQS, the DLQ is setup on SQS side
3. With SNS, the DLQ is setup on lambda side
4. SNS + SQS -> fanout pattern
5. We can react to S3 events like Created, modified, removed
    1. Like generating thumbnail for image uploaded
    2. Can have async call to lambda
6. S3 event notifications are usually delivered in seconds but can sometime take a minute or longer
7. Blocking an IP
    1. NACL at VPC level - deny rule
    2. Security group at EC2 level  - allow rule
    3. Optional firewall software in EC2
    4. ALB - connection termination
    5. NLB - doesn’t have connection termination, use EC2 security group
    6. WAF - Web application firewall - expensive
8. High performance computing (HPC)
    1. Perform genomics, ML, DL. Financial risk monitoring
    2. Data management & transfer
        1. AWS direct connect
        2. Snowball & snowmobile
        3. DataSync
    3. Compute and networking
        1. EC2 instance
            1. CPU, GPU optimised
            2. ASG
            3. Placement group of type cluster for best network performance
            4. Enhanced networking (SR-IOV)
                1. Higher bandwidtjh, 
                2. Elastic Network Adapter (ENA) upto 100Gbps
                3. Intel 82599 VF - legacy
            5. Elastic Fabric Adapter (EFA)
                1. Improved ENA
                2. Only for Linus 
                3. Create for inter-node communications, tightly coupled workloads
                4. Leverages Messaging Passing interface (MPI) standard
                5. Bypasses the underlying linux OS to provide latency
    4. Storage
        1. Instance attached storage
            1. Instance store
            2. EBS
        2. Network storage
            1. S3
            2. EFS
            3. FSx for lustre
                1. HPC for linux
                2. Backed by S3
    5. Automation and orchestration
        1. AWS Batch
            1. Supports multi-node parallel jobs which enables you to run single jobs that span multiple EC2 instances
        2. AWS parallelCluster
            1. Open source cluster management tool to deploy HPC on AWS
            2. Configure with text files
            3. Automate creation of VPC, Subnet, cluster type and instance types
9. We cannot use ALB with bastion host, Need to use NLB because SSH is layer 4 and ALB is layer 7
    1. If 1 bastion host use Elastic IP
    2. If 2 bastion host use NLB
10. CICD
    1. Code- AWS codeCommit
    2. Build & test - AWS codeBuild
    3. Deploy & provision - 
        1. Elastic Beanstalk
        2. Code deploy & cloudformation
    4. Code pipeline for all steps combined
