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
