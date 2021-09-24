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
