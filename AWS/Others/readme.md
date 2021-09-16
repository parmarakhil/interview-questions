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
