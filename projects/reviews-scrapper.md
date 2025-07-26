# Reviews API Microservice

## Project Overview

A scalable microservice that centralizes and automates the retrieval, management, and analysis of customer reviews from Google Maps. The system provides versioned RESTful endpoints for querying review data, triggering updates, and managing company records through background scraping tasks with robust error handling and health monitoring.

## Technical Responsibilities

- **Full-Stack Development**: End-to-end design and implementation of a production microservice with CI/CD integration
- **API Architecture**: Designed and implemented secure RESTful endpoints with API key authentication
- **Distributed Processing**: Built asynchronous task workflows for scalable data processing
- **System Reliability**: Implemented comprehensive health checks, retry mechanisms, and error handling strategies

## System Architecture

### Application Structure
- **Modular Design**: FastAPI application with versioned sub-applications (`/v1`) and context-managed lifespan hooks
- **Configuration Management**: Centralized environment variable handling for database, Redis, and worker settings
- **Distributed Tasks**: Celery worker architecture for decoupled, long-running background operations
- **Web Scraping Engine**: Playwright-driven automation with BeautifulSoup parsing and data normalization

### Key Technical Features
- Automatic retries with exponential backoff
- Dynamic content handling for changing web structures
- Concurrent processing with rate limiting controls
- Structured logging and error tracking

## Technology Stack

- **Backend**: Python, FastAPI, custom framework for API patterns
- **Web Automation**: Playwright (headless browser), BeautifulSoup, lxml
- **Task Management**: Celery with Redis broker
- **Database**: SQLAlchemy ORM with relational database
- **DevOps**: Docker containerization, GitHub Actions CI/CD
- **Utilities**: Python-dateutil, base64/JSON serialization

## Key Technical Achievements

### Resilient Web Scraping
- Built configurable scraper handling dynamic DOM changes
- Implemented regex-based text extraction adapting to layout shifts
- Created data normalization pipeline for timestamps and ratings

### Scalable Processing Architecture
- Designed fail-fast startup with database health validation
- Implemented Redis-based locking for serialized operations
- Built API-triggered and scheduled task dispatching system

### Production-Ready Design
- Structured versioned API with backward compatibility
- Comprehensive error handling and monitoring
- Automated deployment pipeline with container orchestration

## Technical Challenges & Solutions

### Dynamic Content Management
**Challenge**: Frequent DOM structure changes in target web pages  
**Solution**: Combined robust CSS selectors with adaptive regex extraction patterns

### Concurrency Control
**Challenge**: Preventing system overload and rate limiting  
**Solution**: Implemented process flags and Redis-based distributed locking

### Observability & Reliability
**Challenge**: Production error tracking and system monitoring  
**Solution**: Structured logging framework with contextual error reporting and automated alerting

## Project Impact

Delivered a production microservice (v2.0.1) providing real-time review data ingestion and analysis. The system enables automated monitoring and analytics with minimal manual intervention, demonstrating expertise in distributed systems, web automation, and scalable API design.
