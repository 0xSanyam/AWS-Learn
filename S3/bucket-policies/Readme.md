## Create buckets

```sh
aws s3 mb s3://bucket-policy-sanyy
aws s3 mb s3://deny-bucket-sany
```

## Adding objects in the buckets

```sh
echo "Hello" > hello.txt
aws s3 cp hello.txt s3://bucket-policy-sanyy
aws s3 cp hello.txt s3://deny-bucket-sany
```

## Create buckets policy

<!-- https://awscli.amazonaws.com/v2/documentation/api/latest/reference/s3api/put-bucket-policy.html -->
```sh
aws s3api put-bucket-policy --bucket bucket-policy-sanyy --policy file://policy.json
aws s3api put-bucket-policy --bucket deny-bucket-sany --policy file://deny-policy.json
```

## Verifying the policy change

```sh
aws s3api get-bucket-policy --bucket bucket-policy-sanyy 
aws s3api get-bucket-policy --bucket deny-bucket-sany
```

## Testing from another account's Cloudshell

```sh
aws s3 ls s3://bucket-policy-sanyy
aws s3 ls s3://deny-bucket-sany # An error occurred (AccessDenied) when calling the ListObjectsV2 operation: Access Denied

touch putting.txt
aws s3 cp putting.txt s3://bucket-policy-sanyy
aws s3 ls s3://bucket-policy-sanyy
```

## Cleanup

```sh
aws s3 rm s3://bucket-policy-sanyy --recursive
aws s3 rb s3://bucket-policy-sanyy

aws s3 rm s3://deny-bucket-sany --recursive
aws s3 rb s3://deny-bucket-sany
```