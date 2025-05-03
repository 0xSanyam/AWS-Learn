## Create a bucket

```sh
aws s3 mb s3://metadata-sany-12345
```

### Create a new file

```sh
echo "Hello Earth" > earth.txt
```

## Upload file along with metadata

```sh
aws s3api put-object --bucket metadata-sany-12345 --key earth.txt --content-type plain/txt --body earth.txt --metadata Planet=Earth
```

## Get metadata by head object without having to download the object

```sh
aws s3api head-object --bucket metadata-sany-12345 --key earth.txt
```

## Cleanup

```sh
aws s3 rm s3://metadata-sany-12345/earth.txt
aws s3 rb s3://metadata-sany-12345
```