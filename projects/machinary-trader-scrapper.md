# Machinery Trader Scraper

## Project Overview

A scalable backend microservice providing centralized RESTful APIs for managing equipment dealers and their machine inventories. The system integrates with external inventory sources to automatically scrape and update machinery listings, ensuring downstream applications receive up-to-date data for a heavy-equipment marketplace.

## Technical Architecture

### System Design
* **Modular service layers**:
  * **Configuration** modules load environment settings, database connections, logging, and queueing parameters
  * **Controllers** handle request validation, session management, and error mapping
  * **Models & Schemas** separate persistence (ORM) from data-transfer objects (Pydantic), including JSONB fields for flexible specs
  * **Tasks** implement asynchronous scraping pipelines via Celery, with retry logic and upsert utilities

### API Framework
* Built on FastAPI extended by lightweight routing abstraction
* Mounted under `/v1` for versioning support
* Includes health-check endpoints for monitoring

### Data Flow
* HTTP requests enter controllers and use SQLAlchemy sessions (read/write separation) to interact with PostgreSQL
* Celery tasks run in background—fetching dealer inventory URLs, parsing HTML with BeautifulSoup, and upserting machines
* Custom exception classes unify error responses
* Retry wrappers safeguard against transient network or parsing failures
* Dependency injection isolates testable components

## Technology Stack

### Core Technologies
* **Backend**: Python 3.11, FastAPI, Pydantic
* **Database**: PostgreSQL with SQLAlchemy ORM, JSONB for semi-structured data
* **Async Processing**: Celery with Redis broker
* **Web Scraping**: requests, BeautifulSoup4
* **Infrastructure**: Docker, Docker Compose, GitHub Actions CI/CD

### Supporting Libraries
* Custom utility libraries for environment management, database operations, logging, and API abstractions

## Key Features & Implementation

### Dealer Management System
* Idempotent CRUD endpoints with Pydantic validation
* Seamless inventory URL management
* API-key based authentication for all endpoints

### Automated Inventory Synchronization
* Celery-based pipeline for periodic machine listing updates
* Retry logic and error logging for fault tolerance
* Efficient batch upsert operations to minimize database load
* Dynamic URL parameterization for different dealer formats

### Flexible Data Schema
* PostgreSQL JSONB fields for evolving machine specifications
* Typed schema models exposed to client applications
* Separation of persistence models from data transfer objects

### Monitoring & Reliability
* Health-check endpoints for service monitoring
* Custom exception handling with unified error responses
* Containerized deployment with automated CI/CD pipelines

## Technical Challenges Solved

### Variable HTML Structures
* Abstracted parsing logic into retry-wrapped utilities
* Early detection system for parse errors
* Robust handling of frequent markup changes

### Database Optimization
* Optimized ORM queries with selective joins and indexed filters
* Bulk upsert utilities for consolidated database operations
* Read/write session separation for improved performance

### Configuration Management
* Centralized environment variable registration and loading
* Consistent behavior across development, CI, and production environments

### Error Handling Consistency
* Unified synchronous and asynchronous error handling
* Custom exception-to-dict converters for API predictability

## Project Impact

* Achieved 90%+ automation of machine listing updates
* Eliminated manual inventory management processes
* Provides reliable data pipeline for marketplace applications and analytics
* Significantly reduced operational overhead while improving data accuracy
