# Create a bucket

```sh
aws s3 mb s3://new-encryption-sany
```

### Creating/Enabling the key with KMS's AWS Managed Keys

> Putting an object in a bucket from AWS console and choosing KMS key and then from the drop down selecting the key having aws/s3 as the alias and uploading it.
 
> Then in KMS console, under AWS managed keys we can see that key and using it for this script as customer keys incur $1 per month.

>[!Important]
> The key chosen should be on the same region as the bucket

### Creating a file

```sh
echo "Hello file" > file.txt
```

## Putting the object in the bucket with SSE-KMS encryption

```sh
aws s3api put-object --bucket new-encryption-sany \
--key file.txt --body file.txt \
--server-side-encryption aws:kms \
--ssekms-key-id redacted
```

### Checking the object and verifying the encryption method

```sh
aws s3api head-object --bucket new-encryption-sany --key file.txt --output json
```

## Putting a object in bucket with SSE-C encryption

https://catalog.us-east-1.prod.workshops.aws/workshops/aad9ff1e-b607-45bc-893f-121ea5224f24/en-US/s3/serverside/ssec

```sh
echo "Hello SSE-C" > sse-c.txt

openssl rand -out sse-c.key 32

aws s3 cp sse-c.txt s3://new-encryption-sany/sse-c.txt --sse-c AES256 --sse-c-key fileb://sse-c.key
```

### Downloading and checking the encrypted file

```sh
aws s3 cp s3://new-encryption-sany/sse-c.txt ssec-downloaded.txt --sse-c AES256 --sse-c-key fileb://sse-c.key

cat ssec-downloaded.txt
```

# Cleanup

```sh
aws s3 rm s3://new-encryption-sany --recursive
aws s3 rb s3://new-encryption-sany
```