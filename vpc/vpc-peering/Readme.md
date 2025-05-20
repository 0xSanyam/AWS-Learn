# Create two VPCs from the AWS console

# Initiate peering connection

```sh
aws ec2 create-vpc-peering-connection --vpc-id vpc-axxxxxxxxxxxx --peer-vpc-id vpc-bxxxxxxxxxxxx
```

# Accept peering connection

```sh
aws ec2 accept-vpc-peering-connection --vpc-peering-connection-id pcx-xxxxxxxxxxxxxxxxxxxx 
```

# Creating routes for both

```sh
aws ec2 create-route --route-table rtb-axxxxxxxxxxxx --destination-cidr-block 12.0.0.0/16 \
--vpc-peering-connection-id pcx-09e3956a7835b6abc

aws ec2 create-route --route-table rtb-bxxxxxxxxxxxx --destination-cidr-block 10.0.0.0/16 \
--vpc-peering-connection-id pcx-09e3956a7835b6abc
```

# Launch two EC2 instances via templates after downloading them and then uploading via the AWS console in CloudFormation

# Cleanup

Delete everything made through AWS console