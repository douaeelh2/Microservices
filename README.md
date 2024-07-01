# Microservices Architecture Documentation

# Description
This documentation provides a comprehensive guide to understanding, implementing, and managing a microservices architecture, focusing on building microservices in Java using Spring Boot and related technologies.

# Table of Contents
- [Introduction to Microservices](#introduction-to-microservices)
    - [What are Microservices?](#what-are-microservices)
    - [Microservices vs. Monolithic Architecture?](#microservices-vs.-monolithic-architecture?)
    - [How do Microservices work?](#how-do-microservices-work)
    - [Key Components of a Microservices Architecture](#key-components-of-a-microservices-architecture)
- [Creating Microservices in Java Using Spring Boot](#creating-microservices-in-java-using-spring-boot)
    - [Spring Boot Microservices Architecture](#spring-boot-microservices-architecture)
    - [What is Spring Cloud?](#what-is-spring-cloud)
- [Middleware and Microservices](#middleware-and-microservices)
    - [SOAP](#soap)
    - [REST](#rest)
    - [GraphQL](#graphql)
    - [gRPC](#grpc)
- [What is a Broker ?](#what-is-a-broker)
    - [Utility of Brokers in Microservices](#utility-of-brokers-in-microservices)
    - [Common Message Brokers](#common-message-brokers)
- [Microservices Communication](#microservices-communication)
    - [Using RestTemplate](#using-resttemplate)
    - [Using WebClient](#using-webclient)
    - [Using Spring Cloud Open Feign](#using-spring-cloud-open-feign)
- [Configuration and Service Discovery](#configuration-and-service-discovery)
    - [Spring Cloud Config Server](#spring-cloud-config-server)
    - [Spring Cloud Netflix Eureka-based Service Registry](#spring-cloud-netflix-eureka-based-service-registry)
- [API Gateway](#api-gateway)
    - [Spring Cloud API Gateway](#spring-cloud-api-gateway)
    - [API Gateway with Automatic Routes Mapping](#api-gateway-with-automatic-routes-mapping)
    - [Global Filter Example](#global-filter-example)
- [Event-Driven Microservices](#event-driven-microservices)
    - [Using Spring Boot and Kafka](#using-spring-boot-and-kafka)
    - [With RabbitMQ Example](#with-rabbitmq-example)
    - [With Apache Kafka Example](#with-apache-kafka-example)
    - [REST API Example](#rest-api-example)
    - [Spring Cloud Stream Example](#spring-cloud-stream-example)
- [Spring Cloud Tutorials](#spring-cloud-tutorials)
    - [Config Example Tutorial](#config-example-tutorial)
    - [OpenFeign Example Tutorial](#openfeign-example-tutorial)
    - [LoadBalancer Example](#loadbalancer-example)
    - [Gateway Tutorial](#gateway-tutorial)
    - [Netflix Eureka: Step-by-Step](#netflix-eureka-step-by-step)
    - [Circuit Breaker: Step-by-Step](#circuit-breaker-step-by-step)
- [Securing Spring Boot Microservices](#securing-spring-boot-microservices)
    - [Security with JWT Authentication](#security-with-jwt-authentication)
    - [Secure with Keycloak](#secure-with-keycloak)
    - [Securing with OAuth2](#securing-with-oauth2)
- [Best Practices](#best-practices)
    - [For Spring Boot Microservices](#for-spring-boot-microservices)
    - [Java Spring Boot Best Practices](#java-spring-boot-best-practices)
    - [Design Patterns](#design-patterns)
    - [Saga Design Pattern](#saga-design-pattern)
- [Spring Boot Microservices Project](#spring-boot-microservices-project)
- [Conclusion](#conclusion)
- [References](#references)

# 1. Introduction to Microservices

# What are Microservices?

![microservices](https://github.com/douaeelh2/Microservices/assets/127549220/6dbfa4d8-87e5-4a2f-9541-c8efb6a31ef4)

- Microservices are a software architectural style in which a large application is built as a collection of small, independent services that communicate with each other over a network.

- Each service is a self-contained unit of functionality that can be developed, tested, and deployed independently of the other services. This allows for more flexibility and scalability than a monolithic architecture, where all the functionality is contained in a single, large codebase.

- Microservices can be written in different programming languages and use different technologies as long as they can communicate with each other through a common API.

- Microservices are designed to be loosely coupled, meaning that changes to one service should not affect the other services. This makes it easier to update, maintain, and scale the application. Microservices architecture is best suited for large and complex applications that need to handle a high volume of traffic and be scaled horizontally.




# Microservices vs. Monolithic Architecture



| Feature/Aspect                    | Microservices Architecture                                                                 | Monolithic Architecture                                      |
|-----------------------------------|---------------------------------------------------------------------------------------------|--------------------------------------------------------------|
| **Definition**                    | Architecture where the application is composed of small, independent services              | Architecture where the application is built as a single, unified unit |
| **Service Independence**          | Each service can be developed, deployed, and scaled independently                           | All components are interconnected and must be deployed together |
| **Scalability**                   | Allows individual services to be scaled independently based on demand                        | Requires scaling the entire application, even if only part of it needs more resources |
| **Development**                   | Enables development using different technologies and languages for different services       | Typically uses a single technology stack throughout the application |
| **Deployment**                    | Services can be deployed independently, leading to faster and more frequent releases        | Deployment requires building and deploying the entire application, which can slow down release cycles |
| **Fault Isolation**               | Failures are isolated to individual services, reducing the impact on the overall system     | Failures can affect the entire application, leading to system-wide downtime |
| **Flexibility**                   | High flexibility in choosing technology stacks and frameworks for different services         | Limited flexibility as the same technology stack is used across the application |
| **Complexity**                    | Increased complexity in managing inter-service communication, data consistency, and deployment | Simpler to develop and deploy as a single unit, but can become complex as the application grows |
| **Performance**                   | Can optimize performance at a granular level, but inter-service communication can introduce latency | Generally performs well initially, but can degrade as the application scales |
| **Maintenance**                   | Easier to update, maintain, and refactor individual services without affecting the entire system | Harder to maintain as changes to one part of the application can impact other parts |
| **Team Organization**             | Teams can be organized around individual services, promoting ownership and faster development | Teams typically work on the same codebase, which can lead to coordination challenges |
| **Testing**                       | Each service can be tested independently, simplifying testing processes                      | Requires testing the entire application, which can be time-consuming and complex |
| **Data Management**               | Decentralized data management, each service manages its own data                              | Centralized data management, all parts of the application share the same database |
| **Examples of Use**               | Large, complex, and scalable applications, such as Netflix, Amazon, and Uber                 | Smaller applications or those with tightly coupled components, such as simple web applications or internal tools |


# How do Microservices work?

![Monolithic-to-Microservices](https://github.com/douaeelh2/Microservices/assets/127549220/3cf2c04b-7a47-4090-8509-bbd447070608)


Microservices work by breaking down a complex application into smaller, independent pieces that communicate and work together, providing flexibility, scalability, and easier maintenance, much like constructing a city from modular, interconnected components.

- ### Modular Structure
    - Microservices architecture breaks down large, monolithic applications into smaller, independent services.
    - Each service is a self-contained module with a specific business capability or function.
    - This modular structure promotes flexibility, ease of development, and simplified maintenance.

- ### Independent Functions
    - Each microservice is designed to handle a specific business function or feature.
    - For example, one service may manage user authentication, while another handles product catalog functions.
    - This independence allows for specialized development and maintenance of each service.

- ### Communication
    - Microservices communicate with each other through well-defined Application Programming Interfaces (APIs).
    - APIs serve as the interfaces through which services exchange information and requests.
    - This standardized communication enables interoperability and flexibility in integrating services.

- ### Flexibility
    - Microservices architecture supports the use of diverse technologies for each service.
    - This means that different programming languages, frameworks, and databases can be chosen based on the specific requirements of each microservice.
    - Teams have the flexibility to use the best tools for their respective functions.

- ### Independence and Updates
    - Microservices operate independently, allowing for updates or modifications to one service without affecting the entire system.
    - This decoupling of services reduces the risk of system-wide disruptions during updates, making it easier to implement changes and improvements.
    - Also Microservices contribute to system resilience by ensuring that if one service encounters issues or failures, it does not bring down the entire system.

- ### Scalability
    - Microservices offer scalability by allowing the addition of instances of specific services.
    - If a particular function requires more resources, additional instances of that microservice can be deployed to handle increased demand.
    - This scalability is crucial for adapting to varying workloads.

- ### Continuous Improvement
    - The modular nature of microservices facilitates continuous improvement.
    - Development teams can independently work on and release updates for their respective services.
    - This agility enables the system to evolve rapidly and respond to changing requirements or user needs.

# Key Components of a Microservices Architecture

- ### Core Services: 
Each service is a self-contained unit of functionality that can be developed, tested, and deployed independently of the other services.
Service registry: A service registry is a database of all the services in the system, along with their locations and capabilities. It allows services to discover and communicate with each other.

- ### API Gateway: 
An API gateway is a single entry point for all incoming requests to the microservices. It acts as a reverse proxy, routing requests to the appropriate service and handling tasks such as authentication and rate limiting.

- ### Message bus: 
A message bus is a messaging system that allows services to communicate asynchronously with each other. This can be done through protocols like HTTP, RabbitMQ, or Kafka.

- ### Monitoring and logging:
Monitoring and logging are necessary to track the health of the services and troubleshoot problems.

- ### Service discovery and load balancing: 
This component is responsible for discovering service instances and directing traffic to the appropriate service instances based on load and availability.

- ### Continuous integration and continuous deployment (CI/CD): 
To make the development and deployment process of microservices as smooth as possible, it is recommended to use a tool such as Jenkins, TravisCI, or CircleCI to automate the process of building, testing, and deploying microservices.


# Middleware and Microservices

Middleware plays a crucial role in microservices architecture by facilitating communication, data exchange, and integration between different services. It acts as a bridge, ensuring that various services can interact seamlessly, even if they are built using different technologies. Middleware helps in handling different aspects like message transformation, protocol conversion, security, and scalability, which are essential for a robust and efficient microservices ecosystem.

| Feature/Aspect              | SOAP                                                 | REST                                                 | GraphQL                                              | gRPC                                                 |
|-----------------------------|------------------------------------------------------|------------------------------------------------------|------------------------------------------------------|------------------------------------------------------|
| **Message Format**          | XML (verbose and rigid)                              | JSON or XML (human-readable)                         | Custom query language (flexible, JSON-like)          | Protocol Buffers (compact, binary)                   |
| **Transport Protocols**     | HTTP, SMTP                                           | HTTP                                                 | HTTP                                                 | HTTP/2                                               |
| **Communication Style**     | Request-Response                                     | Request-Response                                     | Query-Response                                       | Request-Response (Unary, Server/Client Streaming)    |
| **Standards and Security**  | WS-Security, WS-ReliableMessaging, strict standards  | OAuth, JWT, flexible security implementations        | Flexible, schema-based security                      | Built-in authentication, TLS                         |
| **Scalability**             | Moderate scalability, more complex                   | Highly scalable                                      | Highly scalable                                      | Highly scalable                                      |
| **Performance**             | Slower due to XML parsing and processing             | Generally fast, but depends on payload size and processing | Efficient data fetching, reduces over-fetching    | High performance due to efficient binary serialization|
| **Flexibility**             | Less flexible, tightly coupled to XML standards      | Highly flexible, language and platform agnostic      | Very flexible, allows clients to request specific data| Flexible but requires Protocol Buffers definition    |
| **Error Handling**          | SOAP Faults for standardized error reporting         | HTTP status codes, custom error messages             | Errors reported in query responses                   | Detailed error codes, supports retries               |
| **Use Case**                | Enterprise environments requiring robust security    | Public APIs, CRUD operations                         | Complex queries, multiple service interactions       | Internal microservices communication, high throughput|
| **Development Complexity**  | Higher complexity due to extensive standards         | Lower complexity, easier to develop and maintain     | Moderate complexity, requires schema definitions     | Higher complexity, requires Protocol Buffers         |
| **Language Support**        | Broad language support                               | Broad language support                               | Broad language support                               | Broad language support                               |
| **Fault Tolerance**         | Built-in mechanisms for fault tolerance              | High, relies on HTTP retry mechanisms                | High, schema validation reduces errors               | High, supports retries and load balancing            |
| **Tooling and Ecosystem**   | Mature, extensive enterprise-level tools             | Mature, extensive tools and libraries                | Growing ecosystem, modern tooling                    | Mature, supported by major frameworks and tools      |
| **Adoption and Community**  | Widely adopted in enterprise solutions               | Widely adopted across web and mobile applications    | Rapidly growing in modern web applications           | Widely adopted in high-performance systems           |
| **Real-time Support**       | Limited                                              | Limited                                              | Good for real-time data queries                      | Excellent support for real-time communication        |

---

### Key Takeaways
- **SOAP**: Best suited for enterprise environments needing robust security and strict standards.
- **REST**: Ideal for public APIs and CRUD operations due to its simplicity and flexibility.
- **GraphQL**: Useful for applications requiring complex queries and efficient data fetching.
- **gRPC**: Perfect for high-performance, internal microservice communication with low latency requirements.

  

# What is a Broker?

A broker, also known as a message broker, is an intermediary program that translates messages from the formal messaging protocol of the sender to the formal messaging protocol of the receiver. Essentially, it enables communication between different applications or services by routing messages from one service to another.

# Utility of Brokers in Microservices

### Decoupling Services

- Brokers help decouple services, meaning that the services do not need to be aware of each other's location, protocol, or implementation. This decoupling enhances the flexibility and scalability of the system.

### Asynchronous Communication

- Brokers facilitate asynchronous communication, allowing services to send messages without waiting for an immediate response. This improves the system's performance and responsiveness, as services can continue processing other tasks while waiting for responses.

### Load Balancing

- Message brokers can distribute the load evenly across multiple instances of a service, ensuring that no single instance becomes a bottleneck. This load balancing helps improve the reliability and scalability of the system.

### Reliability and Fault Tolerance

- Brokers provide reliability features such as message persistence, ensuring that messages are not lost even if a service or broker instance fails. This fault tolerance is critical for maintaining the integrity and continuity of the system.

### Event-Driven Architecture

- In an event-driven architecture, services communicate by producing and consuming events. Brokers manage these events, enabling real-time processing and reactions to changes within the system.

### Routing and Transformation

- Brokers route messages to appropriate services based on predefined rules and can transform message formats if needed. This simplifies integration between heterogeneous systems.

# Common Message Brokers

- **RabbitMQ:** An open-source message broker using the Advanced Message Queuing Protocol (AMQP), known for flexibility and support for various messaging patterns.
  
- **Apache Kafka:** A distributed event streaming platform handling high-throughput and low-latency data streams, ideal for real-time data pipelines.
  
- **ActiveMQ:** An open-source broker supporting AMQP, MQTT, and STOMP, known for versatility and ease of use.
  
- **Amazon SQS (Simple Queue Service):** A managed message queuing service by AWS, facilitating decoupling and scaling of microservices and serverless applications.
