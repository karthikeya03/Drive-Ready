# API & API Gateway Development Notes

## Introduction

An Application Programming Interface (API) allows one application to communicate with another to fulfill the request of a user. APIs are widely used in various scenarios, from web development to mobile apps.

![API Overview](https://github.com/user-attachments/assets/770bc849-cf12-4521-9251-65fc331170d3)

APIs enable different software systems to communicate and work together by defining a set of rules and protocols. This interaction allows applications to access data and services from other systems.

## Example of API in Use

Consider an API in a hotel scenario where a waiter acts as an API to fulfill the user's requests. The waiter takes the request (order) from the user (customer) to the kitchen (server) and brings back the response (food).

![API in Hotel](https://github.com/user-attachments/assets/321758da-5a1e-4aa8-b720-4dbb2f76b707)

In this example, the waiter (API) interacts between the customer (client) and the kitchen (server), ensuring the customer's requests are met.

## Types of APIs

APIs can be categorized into different types, including Open APIs and Paid APIs.

| Type     | Description                                                  |
| -------- | ------------------------------------------------------------ |
| Open API | Publicly available APIs that can be accessed and used by anyone without any restrictions. |
| Paid API | APIs that require a subscription or payment to access and use their services. |

These APIs do not provide complete server access but only allow interaction with specific functionalities via API endpoints. This ensures no direct access to the database.

![API Access](https://github.com/user-attachments/assets/42a59545-12f4-406c-8cc8-8d2ee5ae6571)

## Displaying Location on a Website

Displaying a location on a website is a type of API usage. For example, integrating Google Maps on your website involves using Google Maps API. The API allows you to embed the map, set markers, and provide location-based information without directly accessing the map data.

## Components of an API

### Request and Response

![Request and Response](https://github.com/user-attachments/assets/2367dbb3-f9f4-478c-a221-432e41822864)

**Request**: The client sends a request to the server. Common HTTP methods include:

- **GET**: Retrieves data from the server. Example: Getting user profile information.
- **PUT**: Updates existing data on the server. Example: Updating username and password in the database.
- **POST**: Sends new data to the server. Example: Creating a new user account.

**Response**: The server sends back a response to the client, which includes the status code and the requested data or an error message. For example, a status code of 200 means the request was successful.

### REST and RESTful

REST stands for Representational State Transfer, and RESTful refers to web services that implement REST principles. These principles include statelessness, cacheability, and a uniform interface, which make the API scalable and easy to use.

![REST and RESTful](https://github.com/user-attachments/assets/00a07ff2-b974-43f7-b3d9-1f1492ab09a3)

## API Response Codes and Statuses

| Code | Status                | Description                                                  |
| ---- | --------------------- | ------------------------------------------------------------ |
| 200  | OK                    | The request was successful.                                  |
| 201  | Created               | The request was successful, and a resource was created.      |
| 202  | Accepted              | The request has been accepted for processing, but the processing is not complete. |
| 204  | No Content            | The request was successful, but there is no content to send for this request. |
| 301  | Moved Permanently     | The URL of the requested resource has been changed permanently. |
| 302  | Found                 | The requested resource resides temporarily under a different URL. |
| 304  | Not Modified          | The resource has not been modified since the last request.   |
| 400  | Bad Request           | The request was invalid or cannot be processed.              |
| 401  | Unauthorized          | Authentication is required and has failed or not been provided. |
| 403  | Forbidden             | The request was valid, but the server is refusing action.    |
| 404  | Not Found             | The requested resource could not be found.                   |
| 500  | Internal Server Error | The server encountered an unexpected condition.              |
| 502  | Bad Gateway           | The server was acting as a gateway or proxy and received an invalid response from the upstream server. |
| 503  | Service Unavailable   | The server is not ready to handle the request.               |

## Example: Instagram API

Instagram provides an API for developers to interact with its platform. Using the Instagram API, developers can fetch user profiles, post photos, and interact with the Instagram community programmatically. For example, you can use the API to get a user's latest photos and display them on your website.

## Postman API Fundamentals

Postman is a popular tool used for API testing and development. It allows you to send requests to an API and inspect the responses. Key features of Postman include:

- Creating and managing API requests
- Organizing requests into collections
- Testing APIs with various HTTP methods (GET, POST, PUT, DELETE)
- Automating tests with scripting

Using Postman, developers can efficiently test and debug their APIs, ensuring they work correctly before deploying them to production.

# Create an API in sandbox - API Gateway Setup and Configuration

## 1. API Gateway Overview

API Gateway allows you to create, publish, maintain, monitor, and secure APIs. It supports different API types:

- **WebSocket API**: Best for real-time applications like chat.
- **REST API**: Suitable for simple GET, PUT, POST, DELETE operations.

![image](https://github.com/user-attachments/assets/9766aa95-068f-4a9e-ab18-a07d98baf3f6)

## 2. Choose API Type

When setting up an API in API Gateway, you can choose between:

- **New API**: Create a brand new API.
- **Import API**: Import an existing API definition.

## 3. API Deployment Options

There are three deployment options:

- **Regional**: The API is deployed in a specific AWS region.
- **Edge-Optimized**: Designed for clients across the globe, using CloudFront to reduce latency.
- **Private**: The API is accessible only within your VPC.

## 4. Creating an API

To create an API:

1. **Create API**: Choose to create a new API.
2. **Create Resources**: Define the resources (paths) and methods for the API.

## 5. Create a Resource

- **Resource Path**: Specify the resource path (e.g., `/users`).
- **Resource Name**: Provide a name for the resource.

## 6. Create a Method

1. **Select Method Type**: Choose HTTP method (e.g., GET, POST).
2. **Integration Type**: For a simple example, choose HTTP integration.
3. **Set up GET Request**:
   - **Select GET Request**: Choose GET as the method.
   - **Copy Public API URL**: Use any public API URL for integration.
  
  ![image](https://github.com/user-attachments/assets/3e8da24d-f2e5-491d-9a9b-eaa8267183a3)


## 7. Pass-Through Behavior

- **Passthrough Behavior**: Determines how the request payload is processed. The default is to pass the request directly to the backend if it matches the integration request format.

## 8. Deploy the API

1. **Deploy API**: Deploy the API to make it available for use.
2. **Select a Stage**: Choose or create a stage (e.g., `dev`, `prod`) for deployment.

![image](https://github.com/user-attachments/assets/34c71b77-7fe7-4dd9-821c-d910a03dce6a)
