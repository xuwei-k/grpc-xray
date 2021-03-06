# grpc-xray
[![Build Status](https://travis-ci.org/xunnanxu/grpc-xray.svg?branch=master)](https://travis-ci.org/xunnanxu/grpc-xray)
[![Sonatype](https://img.shields.io/nexus/r/https/oss.sonatype.org/org.xcorpion/grpc-xray.svg)](https://oss.sonatype.org/content/repositories/releases/org/xcorpion/grpc-xray/)
[![Maven Central](https://img.shields.io/maven-central/v/org.xcorpion/grpc-xray.svg)](https://search.maven.org/artifact/org.xcorpion/grpc-xray)

[Amazon X-Ray](https://aws.amazon.com/xray/) helpers for monitoring gRPC services

![](https://xunnanxu.github.io/2018/11/25/Monitor-gRPC-Microservices-in-Kubernetes-with-Amazon-X-Ray/xray.png)

## How to use

 - Add `org.xcorpion.grpc-xray` to dependency: [Maven Central](https://search.maven.org/artifact/org.xcorpion/grpc-xray)
 
 - To integrate with gRPC server you only need one line if you use gRPC spring:
 
    ```java
    // in your application config class
    @SpringBootApplication(scanBasePackages = {"package.name.of.your.app", "org.xcorpion"})
    ```


 - To integrate with gRPC client you need a different one liner:
 
    ```java
    // when you create your client
    .withInterceptors(new XRayClientInterceptor())
    ```

 - To integrate with regular java servlet based web service:
 
    ```java
    // this assumes spring is used
    @Bean
    public Filter tracingFilter() {
        return new AWSXRayServletFilter(new FixedSegmentNamingStrategy("Your Service"));
    }
    ```
