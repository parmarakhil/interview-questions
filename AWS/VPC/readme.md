# VPC

1. CIDR
    1. Classless Inter Domain Routing
    2. Used for Security group and networking
    3. They have define an IP address range
        1. X.X.X.X/32 -> 32 means 1 IP
        2. X.X.X.X/0 -> 0 means all IP
    4. Has two component
        1. Base IP -> X.X.X.X
            1. Represents an IP contained in the range
        2. The subnet mask (/N)
            1. Defines how many bits can change in the IP
            2. Allows part of the underlying IP to get additional next values from the base IP
            3. /32 -> allows for 1 IP - 2^0=1
            4. /31 -> allows for 2 IP - 2^1=2
            5. /30 -> allows for 4 IP - 2^2=4
            6. /24 -> allows for 256 IP - 2^8=256
2. Default VPC
    1. All new account has a default VPC
    2. New instances are launched in default VPC if no subnet is specified
    3. Default VPC can have internet connectivity and all instances have public IP
    4. We get a public and private DNS name
    5. Subnets belonging to 1 VPC has non overlapping CIDR
3. Own VPC
    1. You can have multiple VPC in a region
    2. Each VPC can have 5 CIDR 
        1. Min Size is /28
        2. Max Size is /16
    3. It is private hence only private IPs are allowed
    4. Your VPC CIDR should not overlap with other networks
4. Subnet
    1. Tied to specific AZ
    2. You can have public and private subnet
    3. AWS reservers 5 IP (first 4 and last 1) in each subnet
        1. 1st -> for Network address
        2. 2nd -> Reserved by AWS for VPC router
        3. 3rd -> Reserved by AWS for mapping Amazon provided DNS
        4. 4th -> Reserved by AWS for some future use
        5. Last one -> Network broadcast address. AWS does not support broadcast in VPC hence address is reserved
    4. Exam Tip -> remember to deduct 5 IP to get available IP
5. Internet gateway & route table
    1. Help VPC instances connect with internet
    2. It is Highly available (HA) and redundant
    3. Must be created separately from VPC
    4. 1 VPC can only be attached to one IGW and vice versa
        1. One Internet gateway per VPC
    5. Internet gateway is also a NAT for the instance that have public IPv4
    6. Internet Gateway on their own don’t allow internet access
        1. Route tables are needed/changed
        2. Route table should point to internet gateway
        3. Instances will get routed through route table
        4. You can have public and private route table
6. Network Address Translation (NAT)
    1. NAT instances — outdated
        1. Allows instances in private subnet to connect to internet
        2. Must be launch in public subnet
        3. Must disable EC2 flag: Source/Destination check
        4. Must have elastic IP attached to it
        5. Route table must be configured to route traffic from private subnet to NAT instance
        6. You need to create EC2 instance for NAT
    2. NAT gateways - New
        1. AWS manages NAT, higher bandwidth, better availability , no administration 
        2. Pay by hour for usage
        3. NAT is created in a specific AZ and uses an Elastic IP
        4. It cannot be used by an instance in that subnet, only be used by other subnets
        5. Requires an IGW (Internet gateway)
        6. 5 Gbps of bandwidth
        7. No security group to manage/required
