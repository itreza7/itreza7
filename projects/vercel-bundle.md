## Vercel Deployment Microservice

### Overview

A Python-based microservice that automates the provisioning, updating, and teardown of customer “dealer” sites on Vercel. It listens for dealer-update events on a Redis-backed queue, validates incoming payloads, orchestrates Vercel project and deployment APIs, and persists metadata in PostgreSQL. Continuous background processes ensure domains are synchronized and verified across environments, enabling near-real-time site updates without manual intervention.

### Role & Responsibilities

* **Lead Engineer** on the design and implementation of the end-to-end service, from message ingestion to API orchestration and persistence.
* Defined and owned the **message consumer**, **task queue**, and **database integration** layers.
* Architected the **Vercel API client**, including payload schemas and error-handling wrappers.
* Configured **Docker** build and **GitHub Actions** CI to produce and publish container images.
* Established robust **logging**, **retry**, and **monitoring** practices to ensure operational reliability.

### Architecture & Design

* **Event-Driven Ingestion**: A continuously running streamer process polls a Redis queue every two seconds, routes messages to named channels, and invokes registered handlers.
* **Asynchronous Task Processing**: Celery workers consume validated events, executing idempotent tasks for create/update/delete workflows against Vercel’s APIs.
* **Persistence Layer**: PostgreSQL stores project metadata (project IDs, environment variables, domain status). SQLAlchemy models and context managers guarantee transactional safety.
* **API Abstraction**: A thin HTTP client wraps Vercel’s REST endpoints, converting between Pydantic-defined schemas and JSON payloads, with centralized error mapping.
* **Domain Orchestration**: Custom logic computes domain order via a topological sorter, handles custom environment creation, and verifies domains in the correct sequence.
* **Containerization & CI/CD**: Dockerfile builds a slim Python 3.11 image; GitHub Actions builds and pushes to a registry on every merge to master.

### Technologies Used

* **Language & Frameworks**: Python 3.11, Pydantic v2, Celery, SQLAlchemy
* **Messaging & Storage**: Redis (queue/backplane), PostgreSQL
* **API & HTTP**: Requests library, custom environment-driven HTTP client
* **DevOps**: Docker, GitHub Actions, DigitalOcean Container Registry
* **Observability**: External logging microservice integration, structured log footprints, retry/exponential backoff

### Key Contributions & Solutions

* **Event Stream Abstraction**: Built a generic Redis-based consumer that supports multiple channels and handlers, enabling future expansion.
* **Schema-Driven Validation**: Employed Pydantic models with alias generators to ensure consistent, type-safe payloads for projects, deployments, domains, and dealers.
* **Idempotent Sync Logic**: Designed create/update/delete flows that first check Vercel state (via HTTP status codes), then conditionally apply changes and update the local database.
* **Domain Verification Workflow**: Utilized a topological sorter to respect inter-domain dependencies, then programmatically invoked verify endpoints and updated verification status.
* **CI/CD Automation**: Automated container image builds and pushes, ensuring that production images always reflect the latest code on the master branch.

### Challenges & Resolutions

* **Rate Limiting & Retries**: Vercel API limits required wrapping calls in a retry decorator with exponential backoff; integrated Celery’s retry mechanism to gracefully handle transient errors.
* **Schema Evolution**: Anticipated payload changes by leveraging Pydantic’s `exclude_unset` and aliasing features, isolating upstream API changes from core logic.
* **Data Consistency**: Concurrent updates between streaming service and Celery tasks were synchronized via database transactions and optimistic commit patterns.
* **Environment Isolation**: Supported preview, development, and production variables by dynamically constructing environment payloads while masking secrets.

### Outcome

Successfully deployed in a production environment, this microservice eliminated manual site management for hundreds of dealer portals. It reduced deployment turnaround time from hours to under five minutes on average, improved reliability through automated retries and structured logging, and provided a scalable foundation for future integrations.
