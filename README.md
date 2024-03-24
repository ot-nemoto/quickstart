# quickstart

## Tutorial

```sh
pulumi version
  # v3.111.1
```

```sh
export AWS_ACCESS_KEY_ID=
export AWS_SECRET_ACCESS_KEY=
```

### Create new project

```sh
pulumi new aws-typescript
```

-   project name: quickstart
-   project description: A minimal AWS Pulumi program
-   stack name: dev
-   aws:region: ap-northeast-1

### Deploy stack

```sh
pulumi up
```

```sh
pulumi stack ls
  # NAME  LAST UPDATE     RESOURCE COUNT  URL
  # dev   46 seconds ago  6               https://app.pulumi.com/ot-nemoto/quickstart/dev
```

```sh
pulumi stack select dev
```

```sh
pulumi stack
  # Current stack is dev:
  #     Owner: ot-nemoto
  #     Last updated: 1 minute ago (2024-03-24 11:10:30.873663562 +0000 UTC)
  #     Pulumi version used: v3.111.1
  # Current stack resources (6):
  #     TYPE                                                       NAME
  #     pulumi:pulumi:Stack                                        quickstart-dev
  #     ├─ aws:s3/bucket:Bucket                                    my-bucket
  #     ├─ aws:s3/bucketPublicAccessBlock:BucketPublicAccessBlock  public-access-block
  #     ├─ aws:s3/bucketOwnershipControls:BucketOwnershipControls  ownership-controls
  #     ├─ aws:s3/bucketObject:BucketObject                        index.html
  #     └─ pulumi:providers:aws                                    default_6_27_0
  #
  # Current stack outputs (2):
  #     OUTPUT          VALUE
  #     bucketEndpoint  http://my-bucket-a4357c5.s3-website-ap-northeast-1.amazonaws.com
  #     bucketName      my-bucket-a4357c5
  #
  # More information at: https://app.pulumi.com/ot-nemoto/quickstart/dev
  #
  # Use `pulumi stack select` to change stack; `pulumi stack ls` lists known ones
```

```sh
aws s3 ls $(pulumi stack output bucketName)
  # 2024-03-24 11:10:31         70 index.html
```

```sh
curl $(pulumi stack output bucketEndpoint)
  # <html>
  #     <body>
  #         <h1>Hello, Pulumi!</h1>
  #     </body>
  # </html>
```

### Destroy stack

```sh
pulumi destroy
```

```sh
pulumi stack rm dev
```
