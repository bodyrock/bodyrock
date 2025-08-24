💻 Tom McDonald (aka bodyrock)

Solution Architect | Full Stack | Cloud | Databases

🚀 About Me

I’m a Solution Architect with 20+ years of experience designing and delivering scalable systems across frontend, backend, and cloud. My expertise spans:

Frontend: React, Angular

Backend: .NET Core, Node.js

Cloud: AWS (Lambda, API Gateway, S3, DynamoDB)

Databases: SQL Server, Oracle, MongoDB

I focus on building secure, high-performing solutions that integrate complex systems and deliver measurable business value.

🛠️ Core Skills

Frontend: React, Angular, TypeScript, JavaScript

Backend: .NET Core, Node.js, RESTful APIs, GraphQL

Cloud: AWS Lambda, API Gateway, S3, CI/CD pipelines

Data: SQL Server, Oracle, MongoDB, data integration & migration

Architecture: Microservices, Event-driven design, Cloud-native solutions

📂 Pinned Projects (Case Studies)
🔹 E-Commerce Modernization Platform

Tech: React, .NET Core, SQL Server, AWS Lambda

Designed a cloud-native architecture for a retail platform handling 10K+ daily transactions.

Built microservices for order management, integrated with payment providers, and modernized frontend UI with React.

Implemented AWS Lambda functions to scale peak shopping season traffic.

# clone sample frontend
git clone https://github.com/bodyrock/ecommerce-frontend-demo
cd ecommerce-frontend-demo
npm install && npm start

# backend API (dotnet core)
git clone https://github.com/bodyrock/ecommerce-api-demo
cd ecommerce-api-demo
dotnet run


flowchart LR
  subgraph Client
    U[User]
    SPA[React SPA]
  end

  subgraph AWS
    CF[CloudFront CDN]
    S3[S3 (static assets)]
    ALB[ALB / API Gateway]
    MS1[.NET Order Service]
    MS2[.NET Catalog Service]
    MS3[.NET Payment Service]
    SQL[(SQL Server)]
    SQS[SQS (async events)]
    L1[(AWS Lambda: promo calc)]
    L2[(AWS Lambda: order events)]
    CW[CloudWatch Logs/Metrics]
  end

  U --> CF --> SPA
  SPA --> ALB
  ALB --> MS1 --> SQL
  ALB --> MS2 --> SQL
  ALB --> MS3 --> SQL

  MS1 -- publish --> SQS --> L2
  SPA -- promo request --> ALB --> L1
  SPA -- static --> S3

  MS1 --> CW
  MS2 --> CW
  MS3 --> CW
  L1 --> CW
  L2 --> CW


🔹 Data Integration Hub

Tech: Node.js, Oracle, MongoDB, Kafka

Architected a real-time data sync between legacy Oracle systems and MongoDB for analytics.

Used Kafka for event streaming and ensured high availability with cluster failover.

Delivered faster insights to business users with a unified data view.

# start kafka + zookeeper
docker-compose up -d zookeeper kafka

# run node.js data sync service
git clone https://github.com/bodyrock/data-integration-demo
cd data-integration-demo
npm install && npm start


flowchart LR
  subgraph Source Systems
    ORA[(Oracle)]
  end

  subgraph Stream Layer
    CDC[CDC / LogMiner]
    K[(Kafka Cluster)]
    S1[Stream Processor (Node.js)]
    S2[Schema Registry]
  end

  subgraph Targets
    MONGO[(MongoDB)]
    BI[[BI/Analytics]]
  end

  ORA -- change logs --> CDC --> K
  K -->|events| S1
  S2 -. schemas .- S1
  S1 --> MONGO
  MONGO --> BI


🔹 IoT Monitoring Dashboard

Tech: Angular, AWS API Gateway, DynamoDB

Designed a monitoring dashboard for thousands of IoT devices.

Built APIs to aggregate sensor data and visualize it in real-time Angular dashboards.

Leveraged AWS serverless stack (API Gateway + Lambda + DynamoDB) for cost-efficient scaling.

# spin up local angular app
git clone https://github.com/bodyrock/iot-dashboard-demo
cd iot-dashboard-demo
npm install && ng serve

# deploy mock lambda function locally
sam local invoke "TelemetryHandler" -e events/telemetry.json


sequenceDiagram
  participant Device as IoT Device
  participant APIGW as API Gateway (REST/WebSocket)
  participant Lambda as AWS Lambda
  participant DB as DynamoDB
  participant Dash as Angular Dashboard

  Device->>APIGW: POST /telemetry {sensor data}
  APIGW->>Lambda: Invoke (ingest)
  Lambda->>DB: PutItem(sensor data)
  Lambda-->>APIGW: 200 OK

  Dash->>APIGW: Connect (WebSocket) / Subscribe
  DB-->>Lambda: DynamoDB Stream (on new data)
  Lambda->>APIGW: Push update (ws message)
  APIGW-->>Dash: Realtime telemetry update


📈 Current Focus

Modernizing legacy apps into cloud-native architectures

Designing full stack solutions that balance scalability & maintainability

Exploring AI-assisted development workflows

🌐 Connect With Me

💼 LinkedIn

🌍 Website / Portfolio

✉️ Email
