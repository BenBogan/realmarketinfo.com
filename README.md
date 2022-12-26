# Setup
### S3 Bucket
- Create S3 Bucket (Public access? bucket policy? CORS policy?)
    - Disable "Block all public access" and create the bucket
    - In properties, enable static website hosting with default settings
    - In permissions, add the following bucket policy: 
>{ 
>    "Version": "2012-10-17",
>    "Statement": [
>        {
>            "Sid": "PublicReadGetObject",
>            "Effect": "Allow",
>            "Principal": "*",
>            "Action": "s3:GetObject",
>            "Resource": "arn:aws:s3:::realmarketinfo-test/*"
>        }
>    ]
>}
    
### DNS
#### Goolge Domains
- Create AWS Route 53 Hosted Zone
- Copy all NS urls
- Add all NS urls to Google Domains custom name servers

#### AWS ACM
- Request certificate for example.com and www.example.com
- Add CNAME records to Route 53 via button in ACM

#### AWS Cloudfront
- Create cloudfront distibution
    - Set Origin to the s3 bucket
    - Set SSL Certificate to the ACM generated cert
    - Set example.com and www.example.com as an Alternate domain names (CNAME) 
    - Set default root object to index.html
    
#### AWS Route 53
- Create 'A' record for example.com with alias pointing to the cloudfront distribution
- Create 'A' record for www.example.com pointing towards example.com
