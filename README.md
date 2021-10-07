# Aircall.io - DevOps technical test

This test is a part of our hiring process at Aircall for [DevOps positions](https://aircall.io/jobs#SystemAdministrator). It should take you between 1 and 6 hours depending on your experience.

__Feel free to apply! Drop us a line with your Linkedin/Github/Twitter/AnySocialProfileWhereYouAreActive at jobs@aircall.io__

## Results :
### Prerequisites
- An AWS account or IAM, with *programmatic* access
- Secrets ***AWS_KEY*** and ***AWS_SECRET*** are set up in *github*

### URL of the application
- **DEV environment** : https://xlhxubq14k.execute-api.eu-west-1.amazonaws.com/dev/image
- **PROD environment** : https://wbwnkacghl.execute-api.eu-west-1.amazonaws.com/prod/image
  
### Address of resized images
- **DEV environment** : https://bsoille-resized-images-bucket-dev.s3.eu-west-1.amazonaws.com/
- **PROD environment** : https://bsoille-resized-images-bucket-prod.s3.eu-west-1.amazonaws.com/

### Try it
In production, given there is an image *img.jpg* in `cwd`:

```shell
curl --location --request POST 'https://wbwnkacghl.execute-api.eu-west-1.amazonaws.com/prod/image' \
--form 'file=@img.jpg' \
--form 's3Key=img.jpg'
```

Then, access your resized images at :
- https://bsoille-resized-images-bucket-prod.s3.eu-west-1.amazonaws.com/img.jpg
- https://bsoille-resized-images-bucket-prod.s3.eu-west-1.amazonaws.com/img.jpg_200
- https://bsoille-resized-images-bucket-prod.s3.eu-west-1.amazonaws.com/img.jpg_75


## Final notes
### Problems 
- There is no TU ; developer should add some
- There are numerous security problems with node dependencies ; developer should have a look


## Summary

An intern in our team has developped an application to resize images. It's working fine.

Unfortunatly, he left the company and we have no documentation or no insights at all about
what he did.

We just have the code.

With the following request to the application, the image is resized, stored and accessible from s3.

```shell
curl --location --request POST 'http://resize.aircall.com/image' \
--form 'file=@img.jpg' \
--form 's3Key=img.jpg'
```

The provided code is working. 

It seems that our intern was using something called Lambda. Don't know what is it.



## What we want ?
Could you please take this code, and deploy it on AWS in a cool way?

Please, make Infra as Code because I heard that it's cool to do so.

You can also make some diagrams if needed.

Technically speaking, we need to get:

- Application URL
- URL of the resized images
- GitHub repo


## Nice to have

- logs
- tracing
- deployment framework
- CI/CD
- auth

Good luck !