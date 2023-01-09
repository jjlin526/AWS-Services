### Amazon API Gateway

Amazon API Gateway is a fully managed service that makes it easy for developers to create, publish, maintain, monitor, and secure APIs at any scale
* APIs act as the "front door" for applications to access data, business logic, or functionality from backend services
* Using API Gateway, you can create **RESTful APIs** and **WebSocket APIs** that enable real-time two-way communication applications
* API Gateway supports containerized and serverless workloads, as well as web applications

API Gateway handles all the tasks involved in accepting and processing up to hundreds of thousands of concurrent API calls, including traffic management, CORS support, authorization and access control, throttling, monitoring, and API version management. API Gateway has no minimum fees or startup costs. You pay for the API calls you receive and the amount of data transferred out and, with the API Gateway tiered pricing model, you can reduce your cost as your API usage scales.

### Why use an API gateway?
* A key benefit of an API gateway is the abstraction of the backend microservices
* An API gateway acts as a proxy for an application’s microservices, exposing the public-facing API endpoints, routing incoming client requests to the relevant services, transforming them as required and aggregating the response data before sending the response to the client

### How does API Gateway Work?  

![image](https://user-images.githubusercontent.com/114364831/211415743-f7df43ae-5b19-416f-ad75-668888959fda.png)
