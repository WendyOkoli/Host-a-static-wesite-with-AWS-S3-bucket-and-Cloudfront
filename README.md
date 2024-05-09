# Hosting a static website using AWS S3 bucket and CloudFront

## Overview 
Create a static website and host it on an S3 bucket(private bucket) but with a public read policy assigned, using CloudFront for CDN.

## Introduction

* Amazon CloudFront

CloudFront is Amazon Web Services (AWS) content delivery network (CDN) service. Its primary function is to accelerate the delivery of web content (such as web pages, images, videos, and other assets) to users worldwide with low latency and high data transfer speeds. It provides global scalability for web applications and static websites hosted on AWS or other origins. It plays a crucial role in optimizing the performance and reliability of web applications and reducing the operational overhead associated with serving content to a global audience.

* Static Website

A static website consists of only client-side technologies such as HTML, CSS, and JavaScript. It doesn't require a server to generate or serve content dynamically.

Utilizing CloudFront as a CDN for this static website improves the performance and reliability of the website by caching content at edge locations worldwide, reducing latency for users across the globe.

### To achieve the overview of this task, I used the following steps below:

1. Create an S3 Bucket on AWS

   On the AWS Management Console, I navigated to the S3 service

   ![S3 Service](/Images/Image1.png)

   I created an S3 bucket with a unique name - `florenceokoli-test`

   ![S3 Bucket Creation](/Images/Image2.png)

   ![S3 Bucket Creation](/Images/Image3.png)

2. Upload files and folders to my S3 bucket

   For this assignment, I used this template [here](https://startbootstrap.com/theme/agency)
   
   I downloaded the template and unzipped it then uploaded it to my S3 bucket.
    
   ![Uplaod website files](/Images/Image5.png)

   ![Uploaded website files](/Images/Image6.png)

3. Set appropriate permissions 

   I unchecked the "block public access" to make the files accessible.

   ![Uncheck Public Access](/Images/Image8.png)

   Next, I added a bucket policy and saved the changes afterwards
   ```
   {
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "PublicReadGetObject",
            "Effect": "Allow",
            "Principal": "*",
            "Action": [ 
               "s3:GetObject"
            ],
            "Resource": [
               "arn:aws:s3:::florenceokoli-test/*"
            ]
        }
    ]
   }


  A snippet of my bucket policy
  ![Bucket Policy](/Images/Image10.png)


   I then enabled static website hosting so the website can serve the static files in my bucket.

   ![Enable Static Website Hosting](/Images/Image9.png)
   
4. Create a CloudFront Distribution

   In the AWS management console, I navigated to the CloudFront service

   ![CloudFront Service](/Images/Image11.png)

   I created a distribution with the origin name `florenceokoli-test.s3.us-east-1.amazonaws.com` with WAF disabled since it is just for testing purposes.

   ![Distribution Origin Name](/Images/Image12.png)

    WAF was disabled below
   ![WAF Disabled](/Images/Image13.png)

   Next, I saved the changes made and distribution was deployed.

   ![Distribution Deployed](/Images/Image14.png)
   After the deployment was completed and the status read enabled, I used the CloudFront domain name `d2o4s4asa3qxqp.cloudfront.net` to access the static website.

   ![Website Hosted with CloudFront](/Images/Image15.png)


## Conclusion

In conclusion, combining Amazon S3 for static website hosting with a public read policy and CloudFront for CDN enhances the accessibility, performance, and scalability of your website. This guide allows you to deliver a fast and reliable web experience to users worldwide while keeping costs low and maintaining simplicity in deployment and management.










