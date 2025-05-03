## Create a bucket

```sh
aws s3 mb s3://change-class-sany
```

## Create a file

```sh
echo "Hello World" > hello.txt
aws s3 cp hello.txt s3://change-class-sany --storage-class STANDARD_IA
```

## Cleanup

```sh
aws s3 rm s3://change-class-sany/hello.txt
aws s3 rb s3://change-class-sany
```