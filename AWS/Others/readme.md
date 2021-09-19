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
11. CloudFormation
    1. Infrastructure as code
    2. A declarative way off outlining AWS infrastructure for any resource
    3. Creates resources in right order with the exact configuration you specify
    4. Code can be versionised using git
    5. Change to infra are reviewed through code
    6. Excellent automative control
    7. You can create many stacks for many apps
    8. Template is uploaded in S3 and then referenced in cloudformation
    9. Building blocks
        1. Resources
            1. AWS resources declared in the template
        2. Parameters
            1. The dynamic inputs for your template
        3. Mappings
            1. Static variables for your template
        4. Outputs
            1. References to what has been created
        5. Conditionals
            1. List fo conditions to perform resource creation
        6. Metadata
        7. Helper
            1. Referencers
            2. Functions
    10. StackSets
        1. Create, update or delete stacks across multiple accounts regions with single operation
        2. Administrator account to create StackSets
        3. Trusted accounts to create, update, delete stack instances from stackSets
        4. When you update a stack set, all associated stack instances are updated thought out all accounts and regions
12. Step functions
    1. Build serverless visual workflow to orchestrate lambda functions
    2. Represent flow as a json state machine
    3. Can have sequence, parallel, conditions, timeouts etc
    4. Can also integrate with EC2, ECS, on-premise,APi gateway
    5. Max execution time is 1 year
    6. Can implement human approval feature
13. Simple Workflow service (SWF)
    1. Corordinate work amongst applications
    2. Code runs on EC2, not serverless
    3. Max 1 year runtime
    4. Concept of “activity step” and “decision step”
    5. Has built in human intervention step
    6. Eg: Order fulfilment
    7. Step functions is recommended to be used for new applications, except
        1. If you need external signals to intervene in the process
        2. If you need child processes to return values to parent processes
14. EMR
    1. Elastic MapReduce
    2. Helps creating Hadoop clusters for big data to analyse and process vast amount of data
    3. Clusters can be made of EC2 instances
    4. Supports Spark, HBase,Presto
    5. EMR takes care of all the provisioning and configuration
    6. Auto-scaling and integrated with spot instances
    7. Use: data processing, ML, web indexing
15. Opsworks
    1. Perform server configuration automatically
    2. It is Managed Chef & puppet
    3. Work great with EC2 & on premise VM
    4. It is alternative to AWS SSM
    5. Managing configuration fo code
    6. Chef - Recipes
    7. Puppet - Manifests
    8. Works across cloud
16. ElasticTranscoder
    1. Convert media files stored in S3 into various formats for tablets. PC, smartphone etc
    2. Features 
        1. Bit rate optimisation, thumbnail, watermarks
    3. Components
        1. Jobs 
        2. Pipeline - Queue that manages the transcoding jobs
        3. Presets - Template for converting media from one format to another
        4. Notifications - eg SNS
    4. Serverless, pay for what you use
17. AWS workspaces
    1. Managed , secure, Cloud desktop
    2. Great to eliminate management of on-premise VDI
    3. On demand, pay per usage
    4. Integrated with Microsoft Active directory
    5. Secure, encrypted, Network isolation
18. AWS Appsync
    1. Store and sync data cross mobile and web apps in real time
    2. Makes use of GrapghQL
    3. Client code can be generated automatically
    4. Integrations with DynamoDB/Lambda
    5. Real-time subscriptions
    6. Offline data synchronisation (Replaces Cognito Sync)
    7. Fine grained security
19. Cost explorer
    1. Visualise, understand and manage AWS cost and usage
    2. Create custom reports
    3. You can analyse both at high level eg total  cost and low level like monthly
    4. You can choose saving plan
    5. Forecast usage upto 12 months based on previous usage

