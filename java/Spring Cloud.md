# Spring Cloud
------------------
https://github.com/in28minutes/spring-microservices/tree/master/03.microservices

- REST, MQ/Kafka
- small autonomous services that work together
- build around business capabilities, auto-deployed, may be written in different languages
- independently deployable, 
- cloud enabled (horizontally scalable)


## Config-Server
Get config from a separate git repository
Web, DevTools, Actuator, Config Client

Currency-exchange-service
```shell script
// Add port to response: so we know which is return the results
ExchangeValue.setPort(environment.getProperty("local.server.port")));

Public interface ExchangeValueRepository extends JpaRepository<ExchangeValue, Long> {
    ExchangeValue findByFromAndTo(String from, String to); // JPA will auto-construct sql from it
```


Currency conversion service

## Feign: replace restTemplate
proxy to make call other service easy


## Ribbon: client side load balance


## Eureka
Discovery service
 

## Zuul: api gateway
@EnableZuulProxy
@EnableDiscoveryClient

- Authentication/authorization/security, 
- rate limits,
- fault tolerance, 
- service aggregation

```shell script
Public class ZuulLoggingFilter extends ZuulFilter { }
```


Call through api gateway
http://localhost:8765/{application-name}/{uri}

@FeignClient(name="netflix-api-gateway")


## Zipkin: Distributed tracing
Zipkin-ui, zipkin-rabbit, zipkin-server


## Sleuth: unique ID for each request -> trace it manually in each app
All services publish to RabbitMQ -> Zipkin listen to it -> persist to DB
- Spring-cloud-starter-sleuth
- Spring-cloud -sleuth-zipkin
- Spring-cloud-starter-bus-amqp


## Spring cloud bus
Change properties in Config -> git commit -> localhost:8080/application/refresh (no need to restart server on 8080) => too much work if we have to refresh 100 servers
```shell script
Spring-cloud-starter-bus-amqp
```
Localhost:8080/bus/refresh: this will refresh all app/services


## Hystrix: fault tolerance
```shell script
<spring-cloud-starter-hystrix>

@EnableHystrix in application
@HystrixCommand(fallbackMethod="fallbackGetUsers") // for each controller api
	fallbackGetUsers: custom method to handle Exception
```


## Microservices characteristics
1. Small
2. independently deployable
3. simple communication: REST
4. stateless: does not hold state
5. automated build and deployment

- Design and Governance of Microservices
    - https://martinfowler.com/microservices/
- 12 Factor App
    - https://12factor.net/
    - https://dzone.com/articles/the-12-factor-app-a-java-developers-perspective
- Spring Cloud
    - http://projects.spring.io/spring-cloud/
