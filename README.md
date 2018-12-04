# Spring Cloud


## Installation on MAC

```shell
# install sdk man and not using brew
curl -s "https://get.sdkman.io" | bash

# install spring boot
sdk use springboot 1.5.3.RELEASE

# install spring cloud
spring install org.springframework.cloud:spring-cloud-cli:1.3.2.RELEASE

```

## Using This Repo

There are four importand directories in this repository.

1. `cloud-config` - This directory contains the configuration used by the Spring Cloud Config Server.
2. `appolo` - This directory contains basic Boot apps that are modified to use Spring Cloud
3. `core` - This directory contains the finalized Boot apps that use Spring Cloud
4.  `config` - This is configuration from Eureka, Config Server, and Zipkin used by the Spring Cloud CLI 

### Prereqs

Before you run the applications in this repository you should install the [Spring Cloud CLI](https://cloud.spring.io/spring-cloud-cli/).

### About The Apps

There are three apps in the `appolo` and four apps in the `core` directories.  

#### Name App
The `name` app will return the value of the `name` property when making an HTTP `GET` request to `/`.

#### Greeting App
The `greeting`app returns a greeting.  You can make a GET request to `/` and it will return `Hello`.  You can also make an HTTP `GET`
and pass a language code to return a greeting for that language.  For example a `GET` to `/es` would return `Hola`.

#### Web App
The `web` app makes a request to both the `greeting` and `name` app to construct the proper greeting when you make a `GET` to `/`.
By changing the `Accept-Language` header you can change the language of the greeting returned.  For example if you set the `Accept-Language` header to `de` the greeting returned will be `Hallo Ryan`.

#### Gateway Web App
This app has the same functionality as the `web` app but leverages the new Spring Cloud Gateway project and uses Spring Boot 2.0.0.
It is only present in the `core` directory.

### Running The Apps

From the root of the repo run
```
$ spring cloud eureka configserver zipkin
```

This will start a Eureka Server, Config Server, and Zipkin.

Then from the `core` directory you can run each of the apps.

NOTE: You do not need to run the Eureka Server, Config Server, and Zipkin when running the app from the `appolo` directory because
they do not use Spring Cloud.
