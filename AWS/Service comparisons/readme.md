# Comparisons

1. VPC Peering vs PrivateLink
    1. These 2 developed separately, but have more recently found themselves intertwined.
        1. VPC Peering - applies to VPC
        2. PrivateLink - applies to Application/Service
    2. With VPC Peering you connect your VPC to another VPC. Both VPC owners are involved in setting up this connection. When one VPC, (the visiting) wants to access a resource on the other (the visited), the connection need not go through the internet.
    3. VPC peering allows VPC resources including ... to communicate with each other using private IP addresses, without requiring gateways, VPN connections, or separate network appliances. ...Traffic always stays on the global AWS backbone, and never traverses the public internet
    4. Inter-Region VPC Peering provides a simple and cost-effective way to share resources between regions or replicate data for geographic redundancy.
    5. PrivateLink provides a convenient way to connect to applications/services by name with added security. You configure your application/service in your VPC as an AWS PrivateLink-powered service (referred to as an endpoint service). AWS generates a specific DNS hostname for the service. Other AWS principals can create a connection to your endpoint service after you grant them permission.
    6. When you create a VPC endpoint service, AWS generates endpoint-specific DNS hostnames that you can use to communicate with the service. These names include the VPC endpoint ID, the Availability Zone name and Region Name, for example, vpce-1234-abcdev-us-east-1.vpce-svc-123345.us-east-1.vpce.amazonaws.com. By default, your consumers access the service with that DNS name
    7. When you create an endpoint, you can attach an endpoint policy to it that controls access to the related service
    8. An endpoint policy does not override or replace IAM user policies or service-specific policies (such as S3 bucket policies). It is a separate policy for controlling access from the endpoint to the specified service.
2. Transit Gateway Vs VPC Peering
    1. Transit Gateway solves the complexity involved with creating and managing multiple VPC peering connections at scale. While this makes TGW a good default for most network architectures, VPC peering is still a valid choice due to the following advantages it has over TGW:
        * Lower cost — With VPC peering you only pay for data transfer charges. Transit Gateway has an hourly charge per attachment in addition to the data transfer fees.
        * No bandwidth limits — With Transit Gateway, Maximum bandwidth (burst) per VPC connection is 50 Gbps. VPC peering has no aggregate bandwidth. Individual instance network performance limits and flow limits (10 Gbps within a placement group and 5 Gbps otherwise) apply to both options. Only VPC peering supports placement groups.
        * Latency — Unlike VPC peering, Transit Gateway is an additional hop between VPCs.
        * Security Groups compatibility — Security groups referencing works with intra-Region VPC peering. It does not currently work with Transit Gateway.
    2. Within your Landing Zone setup, VPC Peering can be used in combination with the hub and spoke model enabled by Transit Gateway.
    3. VPC Peering,
        * Network connections between two VPCs
        * Can connect VPCs in different AWS account.
        * The AWS accounts can be in different AWS region(Inter-Region VPC Peering)
        1. The Good Bites.
            * Lowest cost options
            * Pay only for data transfer
            * No aggregate bandwidth limit.
        2. Things to look out for
            * VPC to VPC connections
            * No transit routing
            * Complex at scale
            * Max 125 connections per VPC

    4. Transit Gateway,
        * Network connections between 1000's of VPC
        * Remove complexity managing multiple connections
        * Hub and spoke design for connecting VPC together
        1. The Good Bites
            * Simplified management of VPC connections.
            * AWS manages the auto scaling and avability needs
            * Supported 1000's of connections
        2. Things to look out for
            * Hourly charges per attachments in addition to data fees
            * Max bandwidth burst to 50 Gbps
            * Infra-region security groups don't support Transit Gateway
    5. AWS Best Practice
        1. AWS VPC Peering
            * VPC peering should be used when the number of VPC's to be connected is less than 10.
            * There is a Max limit 125 peering connections per VPC.
        2. AWS Transit Gateway
            * One transit gateway in a given region
            * Place transit gateway in Network Service Account
            * Use AWS Resource access manager to share a transit gateway for connecting VPCs access multiple account
3. DataSync Vs Storage gateway
    1. One is for optimized data movement (DataSync), and the other is more suitable for hybrid architecture (Storage gateway).
        * AWS DataSync is ideal for online data transfers. You can use DataSync to migrate active data to AWS, transfer data to the cloud for analysis and processing, archive data to free up on-premises storage capacity, or replicate data to AWS for business continuity.
        * AWS Storage Gateway is a hybrid cloud storage service that gives you on-premises access to virtually unlimited cloud storage.
    2. You can combine both services. Use AWS DataSync to migrate existing data to Amazon S3, and then use the File Gateway configuration of AWS Storage Gateway to retain access to the migrated data and ongoing updates from your on-premises file-based applications.
4. Cloudwatch vs Cloudtrail
    1. CloudWatch is a monitoring service for AWS resources and applications. CloudTrail is a web service that records API activity in your AWS account. They are both useful monitoring tools in AWS.
    2. By default, CloudWatch offers free basic monitoring for your resources, such as EC2 instances, EBS volumes, and RDS DB instances. CloudTrail is also enabled by default when you create your AWS account.
    3. With CloudWatch, you can collect and track metrics, collect and monitor log files, and set alarms. CloudTrail, on the other hand, logs information on who made a request, the services used, the actions performed, parameters for the actions, and the response elements returned by the AWS service. CloudTrail Logs are then stored in an S3 bucket or a CloudWatch Logs log group that you specify.
    4. You can enable detailed monitoring from your AWS resources to send metric data to CloudWatch more frequently, with an additional cost.
    5. CloudTrail delivers one free copy of management event logs for each AWS region. Management events include management operations performed on resources in your AWS account, such as when a user logs in to your account. Logging data events are charged. Data events include resource operations performed on or within the resource itself, such as S3 object-level API activity or Lambda function execution activity.
    6. CloudTrail helps you ensure compliance and regulatory standards.
    7. CloudWatch Events is a near real time stream of system events describing changes to your AWS resources. CloudTrail focuses more on AWS API calls made in your AWS account.
    8. Typically, CloudTrail delivers an event within 15 minutes of the API call. CloudWatch delivers metric data in 5 minutes periods for basic monitoring and 1 minute periods for detailed monitoring. The CloudWatch Logs Agent will send log data every five seconds by default.
5. Security group Vs Network Access Control
    1. Security groups 
        1. Acts as a firewall for Associated EC2 instances
        2. Controls both inbound and outbound traffic at the instance level
        3. You can secure your VPC instances using only security groups
        4. Supports allow rules only
        5. It is stateful
        6. Has separate inbound and outbound traffic
        7. Evaluates all rules before deciding whether to allow or Deny traffic
        8. A newly created security group denies all inbound traffic by default and allow all outbound traffic by default
        9. Security groups are associated with network interfaces
    2. Network access control list
        1. Acts as a firewall for associated subnets
        2. Controls both inbound and outbound traffic at the subnet level
        3. They are an additional layer of security
        4. They are stateless
        5. Has separate rules for inbound and outbound traffic
        6. A newly created nACL denies all inbound traffic by default and also deny all outbound traffic by default
        7. Each subnet in your VPC must be associated with a network ACL. If none is associated, the Default NACL is selected
        8. You can associate a network ACL with multiple subnets however a subnet can be associated with only one network ACL at a time
6. IAM policies VS Service Control Policies (SCP)
    1. SCP are mainly used along with AWS Organisation while IAM policies operate at principal level
    2. SCPs do not replace IAM policies, they do not provide actual permission like IAM policies. IAM policies are of two types
        1. Identity based policies - attached to an IAM user, group or role
        2. Resource based policies - attached to an AWS resource like S3 bucket
    3. SCP takes precedence over IAM policies. Even if a principal is allowed to perform an action by IAM policy, an attached SCP can overrode that capability
    4. IAM policies cannot be attached to AWS Organisation
    5. In SCP you choose to either whitelist or blacklist a specific AWS service while an IAM policy can allow or deny actions. Access to any services that isn’t explicitly allowed by the SCP is denied to the AWS accounts associated with SCP. In IAM policy, an explicit allow overrides an implicit deny and an explicit deny overrides an explicit allow
7. Data pipeline Vs database migration service
    1. AWS Data Pipeline helps you to process and move data (ETL) between S3, RDS, DynamoDB, EMR, On-premise data sources.
        1. AWS Data Pipeline can create complex data processing workloads that are fault tolerant, repeatable, and highly available
        2. AWS Data Pipeline launches required resources and tear them down after execution
        3. REMEMBER : AWS Data Pipeline is NOT for streaming data!
    2. AWS Database Migration Service is used to migrate databases to AWS while keeping source databases operational.
        1. Two types of migrations:
            1. Homogeneous Migrations (ex: Oracle to Oracle)
            2. Heterogeneous Migrations (ex: Oracle to Amazon Aurora, MySQL to Amazon Aurora)
        2. important characteristics:
            1. Free for first 6 months when migrating to Aurora, Redshift or DynamoDB
            2. (AFTER MIGRATION) You can keep databases in sync and pick right moment to switch
        3. Important use cases:
            1. Consolidate multiple databases into a single target database
            2. Continuous Data Replication can be used for Disaster Recovery
8. Aurora Vs Dynamodb
    1. Aurora has concept of referential integrity I.e foreign keys while DynamoDB doesn’t have that
    2. Aurora only has immediate consistency while in DynamoDB you can have eventual as well as immediate consistency
    3. Aurora is a relational DBMS model while DynamoDB is Document store and key-value store
    4. Aurora supports server-side scripting while dynamodb  doesn’t
    5. In Aurora, portioning can be done with horizontal partitioning. DynamoDB supports sharing as partitioning method
    6. Aurora supports SQL query language while dynamodb doesn’t
    7. Aurora supports on one replication method - master-slave replication. DynamoDB supports replication methods
    8. Aurora doesn’t offer API for user-defined Map/Reduce methods. DynamoDb also does not offers but maybe implemented via Amazon Elastic MapReduce
9. Scaling policies
    1. Simple Scaling 
        1. Simple scaling relies on a metric as a basis for scaling. 
        2. For example, you can set a CloudWatch alarm to have a CPU Utilization threshold of 80%, and then set the scaling policy to add 20% more capacity to your Auto Scaling group by launching new instances. Accordingly, you can also set a CloudWatch alarm to have a CPU utilization threshold of 30%. When the threshold is met, the Auto Scaling group will remove 20% of its capacity by terminating EC2 instances. 
    2. Target tracking
        1. Target tracking policy lets you specify a scaling metric and metric value that your auto scaling group should maintain at all times. 
        2. Let’s say for example your scaling metric is the average CPU utilization of your EC2 auto scaling instances, and that their average should always be 80%. When CloudWatch detects that the average CPU utilization is beyond 80%, it will trigger your target tracking policy to scale out the auto scaling group to meet this target utilization.
        3. this type of policy assumes that it should scale out your Auto Scaling group when the specified metric is above the target value.
        4. You cannot use a target tracking scaling policy to scale out your Auto Scaling group when the specified metric is below the target value.
        5. The Auto Scaling group scales out proportionally to the metric as fast as it can, but scales in more gradually. 
        6. Lastly, you can use AWS predefined metrics for your target tracking policy, or you can use other available CloudWatch metrics (native and custom). Predefined metrics include the following
            1. ASGAverageCPUUtilization
            2. ASGAverageNetworkIn
            3. ASGAverageNetworkOut 
            4. ALBRequestCountPerTarget
    3. Step Scaling
        1. Step Scaling further improves the features of simple scaling. Step scaling applies “step adjustments” which means you can set multiple actions to vary the scaling depending on the size of the alarm breach. 
        2. When a scaling event happens on simple scaling, the policy must wait for the health checks to complete and the cooldown to expire before responding to an additional alarm. This causes a delay in increasing capacity especially when there is a sudden surge of traffic on your application.
        3. With step scaling, the policy can continue to respond to additional alarms even in the middle of the scaling event.

