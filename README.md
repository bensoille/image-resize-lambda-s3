# Image resize service

This service accepts an image in *POST* http request, and creates 2 resized images from it :
- 200px wide
- 75px wide

Then it uploads these 3 images (the original one and the two resized ones) to some publicly available *S3*

> This *nodejs* service is deployed to *AWS lambda functions*, exposed via *API gateway*

## Prerequisites
- An AWS account or IAM, with *programmatic* access
- Secrets are set up in *github* :
  - ***AWS_KEY*** : the AWS account access key
  - ***AWS_SECRET*** : the AWS account secret key

## Used tools
This toolchain is used for CI/CD :
- [Serverless framework](https://www.serverless.com/) 
- [github actions](https://github.com/features/actions)
- [npm](https://www.npmjs.com/)

## Deployments
This service is deployed automatically on *github* events. See dedicated paragraph below.

### URL of the application
- **DEV environment** : https://xlhxubq14k.execute-api.eu-west-1.amazonaws.com/dev/image
- **PROD environment** : https://wbwnkacghl.execute-api.eu-west-1.amazonaws.com/prod/image
  
### Address of resized images
- **DEV environment** : https://bsoille-resized-images-bucket-dev.s3.eu-west-1.amazonaws.com/
- **PROD environment** : https://bsoille-resized-images-bucket-prod.s3.eu-west-1.amazonaws.com/

### Try it
In production environment, being said that you have an image *img.jpg* in your `cwd`:

```shell
curl --location --request POST 'https://wbwnkacghl.execute-api.eu-west-1.amazonaws.com/prod/image' \
--form 'file=@img.jpg' \
--form 's3Key=img.jpg'
```

Then, access your resized images at :
- https://bsoille-resized-images-bucket-prod.s3.eu-west-1.amazonaws.com/img.jpg
- https://bsoille-resized-images-bucket-prod.s3.eu-west-1.amazonaws.com/img.jpg_200
- https://bsoille-resized-images-bucket-prod.s3.eu-west-1.amazonaws.com/img.jpg_75

## CI / CD
CI is running, some tests are performed on every `push` git command :
- Unit tests (none are there so far)
- Code scanning with [codeQL](https://codeql.github.com/)
- `serverless` file format checking

This service is automatically deployed to `dev` and `prod` environments :
- **on merge in master** : deploy to DEV environment
- **on tag** (beginning with a 'v') : deploy to production

## Final notes

### Problems found
- There is no TU ; developer should add some
- There were security problems with node dependencies, quite fixed by changing `packages-lock` file ; developer should have a look

### Logs
Logs are stored in *cloudWatch*.     
Could be centralized in some *datadog* service and get easier to parse.

### Tracing
Some metrics are displayed in dashboards at *cloudWatch*. Indeed, one dashboard gets created as per environment :
- *DEV* : dev-image-resizeDashboard
- *PROD* : prod-image-resizeDashboard

## Yet to be done
- build some *local* environment with SAM or localstack
- 
