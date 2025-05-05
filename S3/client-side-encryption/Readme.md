## create a bucket

```sh
aws s3 mb s3://client-encrypt-sany
```

## Creating a file

```sh
echo "Hello Client" > client.txt
```

## Encrypting the data and running the encrypt script

https://docs.aws.amazon.com/sdk-for-ruby/v3/api/Aws/S3/EncryptionV2.html
```sh
bundle init
bundle install

bundle exec ruby encrypt.rb
```

## Cleanup

```sh
aws s3 rm s3://client-encrypt-sany --recursive
aws s3 rb s3://client-encrypt-sany
```