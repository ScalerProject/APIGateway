# API Gateway Microservice (Spring Boot)

This project is a production-ready API Gateway microservice built with Spring Boot, Spring Cloud Gateway, and Eureka for service discovery. It is designed to route requests to backend microservices (such as user and product services) and can be extended for additional services.

## Features
- **API Gateway**: Central entry point for routing client requests to backend microservices.
- **Service Discovery**: Integrates with Eureka for dynamic service registration and discovery.
- **Configurable Routing**: Easily add or modify routes to backend services via configuration.
- **Spring Boot**: Leverages Spring Boot for rapid development and deployment.

## Project Structure
```
src/
  main/
    java/com/scaler/apigatewayjan25/
      ApiGatewayJan25Application.java  # Main application entry point
    resources/
      application.properties           # Application configuration
  test/
    java/com/scaler/apigatewayjan25/
      ApiGatewayJan25ApplicationTests.java # Basic context load test
```

## Getting Started

### Prerequisites
- Java 17 or later
- Maven or Gradle
- Eureka Server running (default: `http://localhost:8761/eureka`)

### Configuration
Edit `src/main/resources/application.properties` as needed:

```
spring.application.name=APIGatewayJan25
server.port=7070

eureka.client.registerWithEureka=true
eureka.client.fetchRegistry=true
eureka.client.service-url.defaultZone=http://localhost:8761/eureka
```

#### Example: Adding Routes
Uncomment and modify the following in `application.properties` to enable routing:

```
#spring.cloud.gateway.routes[0].id=productservice
#spring.cloud.gateway.routes[0].predicates[0]=Path=/products/*
#spring.cloud.gateway.routes[0].uri=lb://PRODUCTSERVICEJAN25

#spring.cloud.gateway.routes[1].id=userservice
#spring.cloud.gateway.routes[1].predicates[0]=Path=/users/*
#spring.cloud.gateway.routes[1].uri=lb://USERSERVICEJAN25
```
- `lb://SERVICE_NAME` refers to the logical name registered with Eureka.

### Running the Application

1. **Start Eureka Server** (if not already running).
2. **Build and Run**:
   - With Maven:
     ```sh
     ./mvnw spring-boot:run
     ```
   - With Gradle:
     ```sh
     ./gradlew bootRun
     ```
   - Or build a JAR and run:
     ```sh
     ./mvnw clean package
     java -jar target/apigatewayjan25-*.jar
     ```

The gateway will start on the configured port (default: 7070).

## Extending the Gateway
- **Add new microservices**: Register them with Eureka and add new routes in `application.properties`.
- **Security**: Integrate Spring Security for authentication and authorization.
- **Filters**: Implement custom filters for logging, rate limiting, etc.

## Production Recommendations
- Use a centralized configuration server (Spring Cloud Config) for managing properties.
- Secure endpoints and sensitive routes.
- Enable monitoring and distributed tracing (e.g., with Spring Cloud Sleuth, Zipkin).
- Use containerization (Docker) and orchestration (Kubernetes) for deployment.

## License
MIT or your preferred license.

## Contact
For questions or support, contact your engineering team or maintainer. 