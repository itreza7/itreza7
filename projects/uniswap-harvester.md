# Uniswap Swap Harvester

## Project Overview

A high-throughput ingestion service that captures every swap event on Uniswap v3 using The Graph subgraph as the source of truth. The system populates a MySQL database with normalized transaction and swap records for rapid downstream analytics, enabling on-chain price-impact research and decentralized exchange strategy development.

## Technical Architecture

### Producer-Consumer Pattern
* **Producer** enqueues GraphQL query tasks (block-based or timestamp-based) into Redis
* **Consumer** retrieves tasks, fetches swap data, converts raw GraphQL payloads into ORM objects, and commits them to MySQL

### Task Scheduling & Processing
* **Celery Beat** schedules recurring "latest swap" and historical range crawls
* Automatic chunking of large time windows to prevent timeouts and rate-limits
* Multi-agent crawlers (block, timestamp range, and chunked ranges) ensure full coverage without duplication

### Data Pipeline Components
* **GraphQL Client:** Custom HTTP client with rotating API keys, retry logic, and exponential back-off
* **Domain Conversion Layer:** Transforms nested GraphQL swap objects into flat transaction and swap entities
* **Idempotent Database Writes:** Enforced unique constraints and de-duplication logic to prevent stale records

### Observability & Resilience
* Structured JSON logging via Loguru
* Prometheus metrics for rows inserted, last processed block, and error rates
* Celery retry policy with exponential back-off for transient failures
* Pydantic-based configuration management with environment variable validation

## Technology Stack

* **Backend:** Python 3.11, FastAPI, Celery, SQLAlchemy, Pydantic
* **Data Storage:** MySQL, Redis
* **APIs & Protocols:** GraphQL (via HTTPX), Prometheus metrics
* **Infrastructure:** Docker, Docker Compose, Gunicorn with Uvicorn workers
* **Testing:** pytest, pytest-asyncio, coverage, ruff, black

## Key Technical Achievements

### Performance & Scalability
* **Rate-Limit Management:** Mitigated GraphQL throttling by splitting large time windows into smaller chunks and staggering requests across multiple API keys
* **Horizontal Scaling:** Enabled scalable Celery worker deployment to handle increased swap volume
* **CPU Optimization:** Optimized JSON parsing and database indexing strategies for high-throughput processing

### Data Integrity & Reliability
* **Transactional Consistency:** Ensured data integrity under load through batching and session lifecycle management
* **Error-Tolerant Processing:** Automatic detection of "Too many requests" errors with intelligent retry mechanisms
* **Comprehensive Testing:** Unit, integration, and end-to-end test coverage for configuration, APIs, and pipeline execution

### Operational Excellence
* **Full Containerization:** Docker-based deployment for easy scaling and environment consistency
* **Monitoring & Alerting:** Granular metrics and structured logging for operational visibility
* **Extensible Framework:** Modular task definitions allowing seamless addition of new data-harvesting agents

## Project Impact

Delivered a production-ready swap harvesting service that continuously populates a high-quality dataset of Uniswap v3 swaps. The solution supports horizontal scaling, integrates comprehensive monitoring, and empowers analytics teams to derive on-chain insights with minimal operational overhead. The system processes thousands of swap events daily while maintaining data consistency and providing real-time observability.
* **Rate-Limit Management:** Mitigated GraphQL throttling by splitting large time windows into smaller chunks and staggering requests across multiple API keys.
* **Data Consistency Under Load:** Ensured transactional integrity and prevented deadlocks by batching inserts and managing session lifecycles.
* **Scalability:** Enabled horizontal scaling of Celery workers to handle increased swap volume, with CPU-bound tasks optimized through efficient JSON parsing and indexing strategies.
* **Visibility & Alerting:** Achieved full operational insight by exposing granular metrics and logs, facilitating rapid troubleshooting and capacity planning.

### Outcome

Delivered a production-ready swap harvesting service that continuously populates a high-quality dataset of Uniswap v3 swaps. The solution is fully containerized for easy deployment, supports horizontal scaling, and integrates seamless monitoring—empowering analytics teams to derive on-chain insights with minimal operational overhead.
