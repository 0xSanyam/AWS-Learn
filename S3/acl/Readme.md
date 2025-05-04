## Create a bucket

```sh
aws s3 mb s3://acl-sany01
```

<!--- https://awscli.amazonaws.com/v2/documentation/api/latest/reference/s3api/put-public-access-block.html) -->
## Turn off Block Public Access for ACLs

```sh
aws s3api put-public-access-block \
--bucket acl-sany01 \
--public-access-block-configuration "BlockPublicAcls=false,IgnorePublicAcls=false,BlockPublicPolicy=true,RestrictPublicBuckets=true"
```

## Check the updated Block Public Access

```sh
aws s3api get-public-access-block --bucket acl-sany01 --output json
```

<!-- https://awscli.amazonaws.com/v2/documentation/api/latest/reference/s3api/put-bucket-ownership-controls.html -->
## Change Bucket Ownership

```sh
aws s3api put-bucket-ownership-controls \
--bucket acl-sany01 \
--ownership-controls="Rules=[{ObjectOwnership=BucketOwnerPreferred}]"
```

## Check the Bucket Ownership

```sh
aws s3api get-bucket-ownership-controls --bucket acl-sany01 --output json 
```

## Change ACLs to allow for a user in another AWS account

```sh
aws s3api put-bucket-acl --bucket acl-sany01 --access-control-policy file:///workspaces/AWS-Learn/S3/acl/policy.json
```

## Access Bucket from other account's Cloudshell

```sh
touch test_upload.txt
aws s3 cp test_upload.txt s3://acl-sany01
aws s3 ls s3://acl-sany01
```

## Cleanup

```sh
aws s3 rm s3://acl-sany01/test_upload.txt
aws s3 rb s3://acl-sany01
```