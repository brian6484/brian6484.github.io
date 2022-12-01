---
layout: post
title: How to upload files to S3 on Spring Boot project (from set-up to controller)
category: AWS
tags:
  - AWS
---

## Intro
[This easy reference](https://devlog-wjdrbs96.tistory.com/323) is
an easy guide but it provides really basic logic so I plan to add on
more complex logic here.


This guide is separated to 2 parts - AWS and Spring
## AWS
Let's get it
## Make S3 bucket on AWS
One thing to note is don't block all public access because if we do,
we can't access it from our Spring Boot project.

Once S3 has been made, make sure your IAM policy includes S3FullAccess
policy or some sort of S3 policy attached to your role.

**Very important** If you do have S3 access, you will have these 2 
important fields - accessKey and secretKey in your IAM role that 
are needed when setting up .yml file.

## build.gradle
Include this dependency
```yaml
dependencies {
    implementation 'org.springframework.cloud:spring-cloud-starter-aws:2.2.6.RELEASE'
}
```

## application.yml
This is where I unnecessarily struggle the most. As I mentioned
in [my post regarding setting up .yml file with S3]()
I will say it again. Please ensure name of variables exactly match!
accessKey is different from access-key!!

Also, **careful not to upload these secret keys** on github!! I 
explained [here](https://brian6484.github.io/git/2022/10/15/gitignore.html) how to add them on .gitignore and prevent them
from being uploaded.

```yaml
cloud:
  aws:
    s3:
      bucket: my.first.example.sss.bucket
      dir: /whatever
    credentials:
      accessKey: xx
      secretKey: xx
    region:
      static: ap-northeast-2
      auto: false
    stack:
      auto: false
```

## Spring Boot
Let's go to our Spring project

### AWS S3 Config
We use 
```java
@Configuration
public class AwsConfig {

    @Value("${cloud.aws.credentials.accessKey}")
    private String accessKey;

    @Value("${cloud.aws.credentials.secretKey}")
    private String secretKey;

    @Value("${cloud.aws.region.static}")
    private String region;

    @Bean
    public AmazonS3 amazonS3() {
        AWSCredentials awsCredentials = new BasicAWSCredentials(accessKey, secretKey);
        return AmazonS3ClientBuilder.standard()
                .withRegion(region)
                .withCredentials(new AWSStaticCredentialsProvider(awsCredentials))
                .build();
    }
}
```

## S3 Service logic
```java
@RequiredArgsConstructor
@Service
public class S3FileService {
    @Value("${cloud.aws.s3.bucket}")
    private String bucket;

    private final AmazonS3 amazonS3;

    public String upload(MultipartFile multipartFile, MemberDto memberDto) throws IOException {
        //for saved file in s3 to have unique names via UUID.randomUUID()
        String s3FileName = UUID.randomUUID() + "-" + multipartFile.getOriginalFilename();

        //inform file's size via ContentLength to S3
        ObjectMetadata objMeta = new ObjectMetadata();
        objMeta.setContentLength(multipartFile.getInputStream().available());

        //s3 api method to open file stream and upload it to S3
        amazonS3.putObject(bucket, s3FileName, multipartFile.getInputStream(), objMeta);

        return amazonS3.getUrl(bucket, s3FileName).toString();
    }

    public void deleteFile(String fileName){
        amazonS3.deleteObject(new DeleteObjectRequest(bucket, fileName));
    }
}
```

## S3 Controller with MultipartFile
```java
@RequiredArgsConstructor
@Service
public class S3FileService {
    @Value("${cloud.aws.s3.bucket}")
    private String bucket;

    private final AmazonS3 amazonS3;

    public String upload(MultipartFile multipartFile, MemberDto memberDto) throws IOException {
        //for saved file in s3 to have unique names via UUID.randomUUID()
        String s3FileName = UUID.randomUUID() + "-" + multipartFile.getOriginalFilename();

        //inform file's size via ContentLength to S3
        ObjectMetadata objMeta = new ObjectMetadata();
        objMeta.setContentLength(multipartFile.getInputStream().available());

        //s3 api method to open file stream and upload it to S3
        amazonS3.putObject(bucket, s3FileName, multipartFile.getInputStream(), objMeta);

        return amazonS3.getUrl(bucket, s3FileName).toString();
    }

    public void deleteFile(String fileName){
        amazonS3.deleteObject(new DeleteObjectRequest(bucket, fileName));
    }
}
```

That is all!!
