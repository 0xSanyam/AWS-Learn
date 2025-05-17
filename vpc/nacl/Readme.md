# Creating an NACL 
https://awscli.amazonaws.com/v2/documentation/api/latest/reference/ec2/create-network-acl.html

```sh
aws ec2 create-network-acl --vpc-id vpc-01840ab521335d14e
```

## Putting a rule

```sh
aws ec2 create-network-acl-entry \
--network-acl-id acl-0fd94a47a037bf342 \
--ingress \
--rule-number 90 \
--protocol -1 \
--port-range From=0,To=65535 \
--cidr-block 174.5.108.3/32 \
--rule-action deny
```

# Deleting the NACL

```sh
aws ec2 delete-network-acl --network-acl-id acl-0fd94a47a037bf342
```