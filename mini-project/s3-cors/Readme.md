# Creating First Website

## Creating a bucket

```sh
aws s3 mb s3://new-cors-sany
```

## Changing Block Public Access

```sh
aws s3api put-public-access-block \
--bucket new-cors-sany \
--public-access-block-configuration "BlockPublicAcls=true,IgnorePublicAcls=true,BlockPublicPolicy=false,RestrictPublicBuckets=false"
```

## Checking the updated Block Public Access

```sh
aws s3api get-public-access-block --bucket new-cors-sany --output json
```

## Creating Bucket Policy

https://awscli.amazonaws.com/v2/documentation/api/latest/reference/s3api/put-bucket-policy.html
```sh
aws s3api put-bucket-policy --bucket new-cors-sany --policy file://policy.json
```

## Verifying the policy change

```sh
aws s3api get-bucket-policy --bucket new-cors-sany
```

## Static website hosting

```sh
aws s3api put-bucket-website --bucket new-cors-sany --website-configuration file://website.json
```

## Uploading index.html and 404.html file

```sh
aws s3 cp index.html s3://new-cors-sany
aws s3 cp 404.html s3://new-cors-sany
```

## Checking the website

```html
http://new-cors-sany.s3-website.ap-south-1.amazonaws.com
```

# Creating Second Website

## Creating a bucket

```sh
aws s3 mb s3://second-cors-sany
```

## Changing Block Public Access

```sh
aws s3api put-public-access-block \
--bucket second-cors-sany \
--public-access-block-configuration "BlockPublicAcls=true,IgnorePublicAcls=true,BlockPublicPolicy=false,RestrictPublicBuckets=false"
```

## Checking the updated Block Public Access

```sh
aws s3api get-public-access-block --bucket second-cors-sany --output json
```

## Creating Bucket Policy

https://docs.aws.amazon.com/AmazonS3/latest/userguide/HostingWebsiteOnS3Setup.html
```sh
aws s3api put-bucket-policy --bucket second-cors-sany --policy file://policy-2.json
```

## Verifying the policy change

```sh
aws s3api get-bucket-policy --bucket second-cors-sany
```

## Static website hosting

```sh
aws s3api put-bucket-website --bucket second-cors-sany --website-configuration file://website-2.json
```

## Uploading index.html and 404.html file

```sh
aws s3 cp index-2.html s3://second-cors-sany
aws s3 cp 404-2.html s3://second-cors-sany
```

## Checking the website

```html
http://second-cors-sany.s3-website.ap-south-1.amazonaws.com
```

# Creating mock responsed API Gateway and testing the endpoint

>[!IMPORTANT]
> [Creating method POST and then the desired javascript response is added under Integration responses]

```sh
curl -X POST -H "Content-Type: application/json" https://0gymm1tsb6.execute-api.ap-south-1.amazonaws.com/prod/hello-cors
```

>[!NOTE]
> The invoke api URL is embeded in index-2.html to test CORS

## Setting CORS on the bucket

https://awscli.amazonaws.com/v2/documentation/api/latest/reference/s3api/put-bucket-cors.html
```sh
aws s3api put-bucket-cors --bucket second-cors-sany --cors-configuration file://cors.json
```

## Enabling CORS on the API resource
>[!IMPORTANT]
> [AWS Console, enabling CORS in the API Resources section]

## veryfying CORS on the bucket

```sh
aws s3api get-bucket-cors --bucket second-cors-sany --output json
```

# Cleanup

Delete the stage and then delete the resource

```sh
aws s3 rm s3://new-cors-sany --recursive
aws s3 rb s3://new-cors-sany

aws s3 rm s3://second-cors-sany --recursive
aws s3 rb s3://second-cors-sany
```