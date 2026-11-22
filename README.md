# Intelligent IT Monitoring & Automated Remediation Platform

An AI-powered IT monitoring platform planned to detect infrastructure anomalies, support incident diagnosis, and enable controlled automated remediation. The proposed architecture uses Spring Boot microservices, Apache Kafka for asynchronous communication, PostgreSQL with pgvector for persistence, and Spring AI with Ollama as the initial local LLM provider.

> **Project status:** This repository is currently at the structure and planning stage. The architecture and capabilities described below are planned; no application services or frontend have been implemented yet.

## Project objectives

- Establish an event-driven foundation for collecting and processing infrastructure telemetry.
- Detect anomalies from normalized logs, metrics, and events.
- Assist incident investigation with AI-generated probable causes and proposed actions.
- Provide a controlled path for authorized remediation, with human oversight and safety boundaries.
- Keep operators informed about incidents, decisions, and remediation outcomes.

## Planned capabilities

- Ingest and normalize logs, metrics, and events from external infrastructure.
- Process telemetry asynchronously and identify anomalous conditions.
- Correlate incident context and use an AI agent to investigate and propose corrective actions.
- Execute only authorized remediation actions through controlled integrations.
- Notify relevant users of incident and action status.
- Expose frontend-facing APIs through a centralized gateway, documented with OpenAPI/Swagger.

These are goals, not implemented features.

## Architecture overview

The planned system is composed of independently deployable backend services. Apache Kafka in KRaft mode is the asynchronous event backbone between services. PostgreSQL with the pgvector extension is planned as the main persistent database. A React frontend will communicate with backend services through Spring Cloud Gateway.

```text
External infrastructure
          │
          ▼
 Monitoring Service ──► Apache Kafka ──► Detection Service
                                               │
                                               ▼
                                      AI Agent Service
                                      (Spring AI + Ollama)
                                               │
                         ┌─────────────────────┴────────────────────┐
                         ▼                                          ▼
              Remediation Service                         Notification Service
                         ▲                                          ▲
                         └────────────── Kafka events ──────────────┘

 React frontend ──► API Gateway ──► backend services
                         │
                         └── PostgreSQL with pgvector (planned persistence)
```

The diagram describes the intended architecture. Service contracts, event schemas, data ownership, security controls, and deployment topology remain to be designed and implemented.

## Planned microservices responsibilities

| Service | Responsibility |
| --- | --- |
| **API Gateway** | Central entry point for frontend requests, planned with Spring Cloud Gateway. |
| **Monitoring Service** | Collects and normalizes logs, metrics, and events from external infrastructure. |
| **Detection Service** | Processes monitoring events and detects anomalies. |
| **AI Agent Service** | Uses Spring AI and an LLM to investigate incidents, identify probable causes, and propose corrective actions. Ollama is the initial planned local provider. |
| **Remediation Service** | Executes authorized corrective actions through controlled infrastructure integrations. |
| **Notification Service** | Sends notifications about incidents, AI decisions, and remediation results. |

Services are intended to communicate asynchronously through Apache Kafka where appropriate. Kafka and service integrations are not configured yet.

## Planned technology stack

- **Backend:** Java 21, Spring Boot, Spring Cloud Gateway, Spring Kafka, Spring AI
- **Messaging:** Apache Kafka in KRaft mode
- **Persistence:** PostgreSQL with pgvector
- **AI provider:** Ollama (initial local provider)
- **Frontend:** React.js with JavaScript (no TypeScript), Tailwind CSS
- **API documentation:** Swagger / OpenAPI
- **Infrastructure:** Docker and Docker Compose

No application code, dependencies, or infrastructure configurations have been generated yet.

## Repository structure

```text
.
├── backend/
│   ├── api-gateway/
│   ├── monitoring-service/
│   ├── detection-service/
│   ├── ai-agent-service/
│   ├── remediation-service/
│   └── notification-service/
├── frontend/
├── infrastructure/
│   ├── docker/
│   ├── kafka/
│   ├── postgresql/
│   └── packet-tracer/
├── docs/
│   ├── architecture/
│   ├── diagrams/
│   └── api/
├── .gitignore
└── README.md
```

The folders above describe the intended layout. Git does not track empty directories, so they will appear in the repository once they contain project files.

## Prerequisites

For planned development and operation, the expected prerequisites are:

- Java Development Kit (JDK) 21
- Maven (version to be selected)
- Node.js and npm (versions to be selected)
- Docker and Docker Compose
- Git

A local Ollama installation will be needed when implementing and running the planned AI integration. These prerequisites are listed for future development; no setup or dependency installation has been performed.

## Development roadmap

All roadmap items are **planned** and are not yet implemented:

1. Define architecture decisions, service boundaries, Kafka event contracts, and security requirements.
2. Add service scaffolding and API/event documentation.
3. Implement telemetry ingestion, normalization, and persistence.
4. Implement event processing and anomaly detection.
5. Add AI-assisted incident investigation using Spring AI and Ollama.
6. Design and implement authorization, approval, auditing, and safety controls for remediation.
7. Add notification workflows and the React operator interface.
8. Create Docker-based local development and deployment configurations.
9. Add automated tests, observability, and operational documentation.

## Current status

Only the root project documentation and ignore rules are being initialized. No Spring Boot services, React application, dependencies, Kafka/PostgreSQL setup, or Docker Compose files are present as part of this initialization.
