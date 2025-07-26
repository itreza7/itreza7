# Automotive Inventory Management Microservice

## Project Overview

A comprehensive inventory management microservice responsible for aggregating, transforming, and exposing automotive dealer inventory data. The system provides RESTful endpoints for inventory feeds management, executes background tasks (VIN decoding, vehicle history processing, photo hashing, valuation data retrieval, record archiving), and offers public search endpoints for vehicle and equipment listings. Implemented as a standalone, Dockerized ASGI service ensuring scalable and reliable inventory data delivery.

## Technical Architecture

### Framework & Design Patterns

* Built on lightweight ASGI framework with abstractions for Application, Router, Route, and Task components
* Modular structure with clear separation of concerns:
  * `api.py` for HTTP endpoints
  * `streamer.py` for real-time data streams
  * `worker.py` for background job processing
  * Class-based modules for functional domains (feed generation, photo processing, data aggregation)

### Scalability & Infrastructure

* **Database**: PostgreSQL for persistent inventory state management
* **Caching & Queuing**: Redis for task queuing and distributed locking
* **Storage**: S3-compatible object storage for feed asset distribution
* **Monitoring**: Health checks, liveness probes, and retry logic for high availability
* **Deployment**: Docker containerization with multi-environment configuration support

## Technology Stack

### Core Technologies

* **Python 3.11** with custom ASGI framework
* **Uvicorn** for high-performance asynchronous server
* **PostgreSQL** for relational inventory data
* **Redis** for message queuing and ephemeral locks
* **S3-compatible storage** for file distribution

### External Integrations

* **SFTP** for automated report exchange
* **Search Engine Integration** for inventory indexing
* **Image Processing Libraries** (Pillow) for photo hashing
* **HTML Parsing** (BeautifulSoup, lxml) for data extraction

### DevOps & Deployment

* **Docker** containerization
* **GitHub Actions** for CI/CD pipeline
* **Environment-driven configuration** management

## Key Technical Achievements

### Dynamic Feed Generation Engine

* Designed flexible pipeline supporting multiple inventory types (vehicles, equipment, parent records)
* Implemented pluggable components for templating, filtering, and count aggregation
* Enabled real-time feed updates with optimized performance

### Scalable Photo Processing System

* Developed photo hashing pipeline handling large image volumes
* Implemented idempotent processing with external upload service integration
* Optimized for concurrent processing and resource efficiency

### Automated Data Integration Workflows

* Built resilient SFTP-based report processing with error handling
* Orchestrated VIN decoding jobs with data validation and alerting
* Implemented retry policies and circuit-breaker patterns for external API reliability

### Advanced Search & Filtering

* Created real-time filter computation system (make, model, year facets)
* Leveraged pre-aggregated counts with dynamic query optimization
* Delivered fast, faceted search experiences for end users

## Technical Challenges & Solutions

### Performance Optimization

* **Challenge**: High throughput requirements for photo processing and feed generation
* **Solution**: Implemented job batching, Redis queue optimization, and database session management to prevent resource contention

### External Dependency Management

* **Challenge**: Unreliable third-party APIs and FTP endpoints
* **Solution**: Introduced retry policies, exponential backoff, and circuit-breaker patterns within task definitions

### Schema Evolution & Compatibility

* **Challenge**: Evolving data schemas requiring backward compatibility
* **Solution**: Implemented API versioning (`/v1`, `/v2`) and centralized schema abstractions for seamless updates

## Project Outcomes

Successfully deployed production-ready microservice serving as authoritative source for automotive inventory data. The system streamlined inventory management processes, automated critical background operations, and provided robust public-facing search capabilities. Established maintainable architecture patterns and comprehensive documentation enabling team scalability and future enhancements.

## Key Metrics & Impact

* Automated processing of large-scale inventory data
* Real-time search capabilities with sub-second response times
* Robust error handling with 99%+ uptime reliability
* Scalable architecture supporting concurrent user loads
