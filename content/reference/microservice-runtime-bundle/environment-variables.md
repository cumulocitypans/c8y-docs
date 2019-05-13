---
weight: 20
title: Environment variables
layout: redirect
---

The following environment variables are available for microservices:

Name  | Details  
--|--
APPLICATION_NAME  |  The name of the microservice application
SERVER_PORT       |  Default open port (80)
MICROSERVICE_SUBSCRIPTION_ENABLED  |  Default value: true
C8Y_BASEURL  |  Platform address (contains port number)
C8Y_BASEURL_MQTT  |  Platform address of the MQTT server (contains port number)
C8Y_MICROSERVICE_ISOLATION  |  Isolation level (MULTI_TENANT or PER_TENANT)
C8Y_BOOTSTRAP_REGISTER  |  Indicator whether the microservice should perform self registration or not. Default value: false
C8Y_BOOTSTRAP_TENANT  |  Bootstrap user tenant, for MULTI_TENANT - microservice owner
C8Y_BOOTSTRAP_USER  |  Bootstrap user name
C8Y_BOOTSTRAP_PASSWORD  |  Bootstrap user password
C8Y_TENANT  |  Application user tenant (available only for PER_TENANT isolation)
C8Y_USER  |  Application user name (available only for PER_TENANT isolation)
C8Y_PASSWORD  |  Application user password (available only for PER_TENANT isolation)
MEMORY_LIMIT  |  Max memory that can be used. Default value: 256M
PROXY_HTTP_HOST  | &nbsp;
PROXY_HTTP_PORT  | &nbsp;
PROXY_HTTP_NON_PROXY_HOSTS  | &nbsp;
PROXY_HTTPS_HOST  | &nbsp;
PROXY_HTTPS_PORT  | &nbsp;
PROXY_SOCKS_HOST  | &nbsp;
PROXY_SOCKS_PORT  | &nbsp;



#### Example usage

Prerequisite: The microservice has been packed and deployed in the Docker repository. Get the microservice image name and tag with the following command:

```shell
$ docker images
```

Run the Docker container for the microservice providing the environment variables:

```shell
$ docker run -e C8Y_BASEURL=<URL> -e C8Y_BOOTSTRAP_TENANT=<BOOTSTRAP_TENANT> -e C8Y_BOOTSTRAP_USER=<BOOTSTRAP_USERNAME> -e C8Y_BOOTSTRAP_PASSWORD=<BOOTSTRAP_USER_PASSWORD> -e C8Y_MICROSERVICE_ISOLATION=MULTI_TENANT -i -t <DOCKER_REPOSITORY_IMAGE>:<TAG>
```

Use a backslash (\\) before special characters such as `&, !, ;, \`.

### Proxy variables

Proxy variables (PROXY_HTTP_HOST, PROXY_HTTP_PORT, ...) are used to set a proxy URL for different protocols. For the microservices written in Java, setting each variable will result in passing the corresponding parameter into the JVM runtime (for detailed information see the [Java Networking and Proxies](https://docs.oracle.com/javase/8/docs/technotes/guides/net/proxies.html)) webpage.

Proxy variables are passed into the microservice environment during installation. The microservice installer passes the variables into the environment according to the following settings:

 - Tenant options in microservice owner tenant
 - Platform application environment variables

Tenant options have higher priority, i.e. if the parameter is set in both places, the value from the tenant option is taken.

The table below contains the options and variables:

| Tenant option              | Platform env variable                          | Microservice env variable |  
|----------------------------|------------------------------------------------|---------------------------|
| proxy.http.host            | MICROSERVICE_RUNTIME_PROXY_HTTP_HOST           | PROXY_HTTP_HOST           |
| proxy.http.port            | MICROSERVICE_RUNTIME_PROXY_HTTP_PORT           | PROXY_HTTP_PORT           |
| proxy.http.non.proxy.hosts | MICROSERVICE_RUNTIME_PROXY_HTTP_NON_PROXY_HOSTS| PROXY_HTTP_NON_PROXY_HOSTS|
| proxy.https.host           | MICROSERVICE_RUNTIME_PROXY_HTTPS_HOST          | PROXY_HTTPS_HOST          |
| proxy.https.port           | MICROSERVICE_RUNTIME_PROXY_HTTPS_PORT          | PROXY_HTTPS_PORT          |
| proxy.socks.host           | MICROSERVICE_RUNTIME_PROXY_SOCKS_HOST          | PROXY_SOCKS_HOST          |
| proxy.socks.port           | MICROSERVICE_RUNTIME_PROXY_SOCKS_PORT          | PROXY_SOCKS_PORT          |

All tenant options have the same category: `microservice.runtime`

For each protocol (HTTP, HTTPS, socks), microservice environment variables are passed into runtime only if the HOST parameter is set. If the HOST parameter is missing, other parameters for the same protocol are not processed.


#### Examples:

##### The microservice owner tenant has the tenant options

```json
{ category: "microservice.runtime", key: "proxy.http.host", value: "10.11.12.13" }
{ category: "microservice.runtime", key: "proxy.http.port", value: "8080" }
```

and there is an environment variable in the platform application:

```properties
MICROSERVICE_RUNTIME_PROXY_HTTP_PORT=8181
```

Deploying and running the microservice inside Docker will result in passing the following variables into the microservice environment (notice PORT value):

```properties
PROXY_HTTP_HOST=10.11.12.13
PROXY_HTTP_PORT=8080
```

##### The microservice owner tenant has the tenant option

```json
{ category: "microservice.runtime", key: "proxy.https.host", value: "10.11.12.13" }
```

and there is an environment variable in the platform application:

```properties
MICROSERVICE_RUNTIME_PROXY_HTTPS_PORT=8181
```

Deploying and running the microservice inside Docker will result in passing the following variables into the microservice environment:

```properties
PROXY_HTTP_HOST=10.11.12.13
PROXY_HTTP_PORT=8181        
```

##### The microservice owner tenant has the tenant options

```json
{ category: "microservice.runtime", key: "proxy.http.port", value: "8080" }
{ category: "microservice.runtime", key: "proxy.http.non.proxy.hosts", value: "localhost" }
```

and proxy HOST is not set (neither in tenant option, nor env variable).

Deploying and running the microservice inside Docker will not pass any proxy environment variable.


##### The microservice owner tenant has the tenant option

```json
{ category: "microservice.runtime", key: "socks.http.host", value: "10.11.12.13" }  
```

Deploying and running the microservice inside Docker will result in passing the following variable into the microservice environment (only host parameter):

```properties
SOCKS_HTTP_HOST=10.11.12.13
```