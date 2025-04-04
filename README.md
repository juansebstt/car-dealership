# Car Dealership CRM System

## Overview

This project is a comprehensive CRM (Customer Relationship Management) system designed specifically for car dealerships. It's built using a microservices architecture with Java and Spring Boot, leveraging cloud services from AWS to provide a scalable, secure, and robust solution. The system integrates with external APIs like Dealercenter, Manheim, and Carfax to provide a complete view of inventory and vehicle history.  It also includes a real-time chat system and integration with an external salesman app to facilitate communication and sales processes.

## Features

* **Inventory Management:**
    * Fetches and displays vehicle inventory from Dealercenter and Manheim.
    * Provides detailed vehicle information, including pricing and specifications.
* **Customer Management:**
    * Stores and manages customer information.
    * Tracks customer interactions and sales history.
* **Sales Tracking:**
    * Records and manages sales transactions.
    * Generates sales reports.
* **Vehicle History:**
    * Integrates with Carfax to provide vehicle history reports.
* **Real-time Chat:**
    * Enables real-time communication between customers and sales staff.
* **Salesman Integration:**
    * Integrates with an external mobile app for in-store salesman interaction.
* **User Authentication and Authorization:**
    * Secure user authentication using JWT and AWS Cognito.
    * Role-based access control.
* **Notifications:**
    * Sends notifications to users via email, SMS, and push notifications using AWS SNS.
* **API Gateway:**
    * Uses AWS API Gateway to manage and secure API requests.
* **Load Balancing:**
    * Uses AWS Application Load Balancer (ALB) to distribute traffic across microservices.
* **Scalability and Reliability:**
    * Microservices architecture deployed on AWS ECS/EKS for scalability and high availability.
* **File Storage**
    * Stores media files (e.g. car images) in AWS S3.

## Architecture

The system is built using a microservices architecture with the following components:

* **API Gateway:** AWS API Gateway
* **Authentication:** AWS Cognito, Spring Security, and JWT
* **Microservices:**
    * Inventory Service (Spring Boot)
    * Customer Service (Spring Boot)
    * Sales Service (Spring Boot)
    * Notification Service (Spring Boot)
    * Chat Service (Spring Boot)
* **Message Queue:** AWS SQS (for decoupling microservices)
* **Database:** AWS RDS (PostgreSQL)
* **File Storage:** AWS S3
* **Load Balancing:** AWS Application Load Balancer (ALB)
* **Container Orchestration:** AWS ECS/EKS

Here's a simplified diagram of the architecture:


# System Architecture

## Overview

This system follows a **microservices-based architecture** deployed on AWS, using **Spring Boot** for backend services and containerized deployments via **ECS/EKS**. Below is the architecture flow:

```plaintext
📱 Client (Web/Mobile App)
   ├──> 🌐 AWS API Gateway (Routes requests, Auth, Rate Limiting)
         ├──> ⚖️ AWS ALB (Application Load Balancer)
               ├──> 🏗️ AWS ECS / EKS (Containerized Microservices)
                     ├── 📦 Inventory Service (Spring Boot)
                     ├── 👥 Customer Service (Spring Boot)
                     ├── 💰 Sales Service (Spring Boot)
                     ├── 🔐 Authentication Service (AWS Cognito)
                     ├── 📢 Notification Service (AWS SNS)
                     ├── 💬 Chat Service (Spring Boot)
                     ├── ... More Services
                           |
                           ├── 🛢️ AWS RDS (PostgreSQL)
                           ├── 🗄️ AWS S3 (File Storage)
```

## Technologies Used

* **Backend:** Java, Spring Boot
* **Frontend:** HTML, CSS, JavaScript, React/Angular/Vue.js (Choose one)
* **Database:** PostgreSQL
* **API Gateway:** AWS API Gateway
* **Authentication:** AWS Cognito, JWT
* **Notification:** AWS SNS
* **Message Queue:** AWS SQS
* **Load Balancing:** AWS Application Load Balancer (ALB)
* **Containerization:** Docker
* **Orchestration:** AWS ECS/EKS
* **Cloud Provider:** AWS

## API Integrations

* Dealercenter API
* Manheim API
* Carfax API

## Getting Started

1.  **Prerequisites:**
    * Java Development Kit (JDK) 17 or higher
    * Maven or Gradle
    * Docker
    * AWS Account
    * AWS CLI
2.  **Clone the repository:**
    ```bash
    git clone [https://github.com/juansebstt/car-dealership]
    cd car-dealership-crm
    ```
3.  **Set up AWS:**
    * Configure AWS CLI with your credentials.
    * Create an RDS instance for PostgreSQL.
    * Create an S3 bucket for file storage.
    * Set up AWS Cognito for user authentication.
    * Set up AWS SNS for notifications.
    * Create an ECS/EKS cluster.
4.  **Build the microservices:**
    ```bash
    ./gradlew build  # or ./mvnw build
    ```
5.  **Run the microservices (using Docker Compose):**
    * Create a `docker-compose.yml` file to define the services.  Example:
    ```yaml
    version: '3.8'
    services:
      inventory-service:
        image: your-repo/inventory-service:latest
        ports:
          - "8081:8080"
        environment:
          - SPRING_DATASOURCE_URL=jdbc:postgresql://[your-rds-instance.amazonaws.com:5432/your-database](https://www.google.com/search?q=https://your-rds-instance.amazonaws.com:5432/your-database)
          - SPRING_DATASOURCE_USERNAME=your-username
          - SPRING_DATASOURCE_PASSWORD=your-password
          - AWS_REGION=your-aws-region
        depends_on:
          - postgres
      # Add other services here (customer-service, sales-service, etc.)
      postgres:
        image: postgres:14
        environment:
          - POSTGRES_USER=your-username
          - POSTGRES_PASSWORD=your-password
          - POSTGRES_DB=your-database
        volumes:
          - postgres_data:/var/lib/postgresql/data
    volumes:
      postgres_data:
    ```
    * Run Docker Compose:
    ```bash
    docker-compose up -d
    ```
6.  **Deploy to AWS ECS/EKS:**
    * Build Docker images for each microservice.
    * Push the images to Amazon ECR.
    * Define ECS/EKS services and deployments.
    * Configure AWS Application Load Balancer to route traffic to your services.

## Configuration

The microservices are configured using Spring Boot's application.properties or application.yml files.  Environment variables are used to configure the application.  Here are some common configuration properties:

* `SPRING_DATASOURCE_URL`:  The URL of the PostgreSQL database.
* `SPRING_DATASOURCE_USERNAME`:  The username for the database.
* `SPRING_DATASOURCE_PASSWORD`:  The password for the database.
* `AWS_REGION`: The AWS region.
* `AWS_ACCESS_KEY_ID`:  Your AWS access key ID.
* `AWS_SECRET_ACCESS_KEY`: Your AWS secret access key.
* `COGNITO_USER_POOL_ID`: Your Cognito User Pool ID.
* `COGNITO_CLIENT_ID`: Your Cognito Client ID.
* `SNS_TOPIC_ARN`: The ARN of the SNS topic for notifications.

## API Documentation

* Use Swagger or OpenAPI to document your APIs.  Spring Boot can automatically generate OpenAPI documentation.

## Contributing

1.  Fork the repository.
2.  Create a new branch.
3.  Make your changes.
4.  Commit your changes.
5.  Push to the branch.
6.  Submit a pull request.

## License

