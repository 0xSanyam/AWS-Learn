# Creating a user with no permissions

Creating a new user with no permissions then generating out access keys
```sh
aws iam create-user --user-name sts-joe
aws iam create-access-key --user-name sts-joe --output table
```

## Copy the access key and secret key

```sh
aws configure
```

Edit the credentials file to change away from default profile
```sh
vim ~/.aws/credentials
```
keys: i, esc, :wq

Then test who the user is now:
```sh
aws sts get-caller-identity --profile sts
```

## Making sure s3 access is not there

```sh
aws s3 ls --profile sts
```

# Creating a Role with CloudFormation

Creating a role that will access a new resource
```sh
chmod u+x bin/deploy
./bin/deploy
```

# Using new user credentials and assuming role

```sh
aws iam put-user-policy \
--user-name sts-joe \
--policy-name STSAssumeRole \
--policy-document file://policy.json
```

```sh
aws sts assume-role \
--role-arn arn:aws:iam::842517499591:role/my-sts-stack-STSRole-RSvSPdKGmd6T \
--role-session-name s3-sts-joe-exercise
--profile sts
```

## Testing the assumed user
```sh
aws sts get-caller-identity --profile assumed
```

## Testing the access to S3 Buckets

```sh
aws s3 ls --profile assumed
```

# Cleanup

> Delete the CloudFormation stack from the console

## Delete the user policy

```sh
aws iam delete-user-policy \
--user-name sts-joe \
--policy-name STSAssumeRole
```

## Delete the access keys now (for access key open the creds file)

```sh
aws iam delete-access-key \
--access-key-id AKIA4IKPUZ3DUKTYLD5C \
--user-name sts-joe
```

## Delete the user

```sh
aws iam delete-user --user-name sts-joe
```