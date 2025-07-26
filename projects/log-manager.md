# Centralized Logging API Microservice

## Project Overview
High-performance RESTful microservice for centralized log ingestion and real-time alerting. Accepts structured log payloads from multiple services, persists data in PostgreSQL, and broadcasts critical events to Telegram channels for immediate incident response.

## Technical Architecture
- **Modular FastAPI Design**: Versioned sub-application (/v1) with async lifespan management for database health validation and graceful startup/shutdown
- **Database Layer**: SQLAlchemy ORM with custom DatabaseInstance supporting read/write separation and connection pooling
- **Asynchronous Processing**: Celery task queue with Redis broker for non-blocking log processing and retry mechanisms
- **Real-Time Alerting**: Telegram Bot API integration with HTML-safe message formatting and multi-tier broadcasting (errors/warnings)
- **Containerization**: Docker deployment with GitHub Actions CI/CD pipeline for automated builds and registry management

## Key Technical Achievements
- **Dynamic Service Routing**: Generic router mapping service identifiers to log model classes, enabling seamless onboarding of new services
- **Resilient Task Processing**: Exponential backoff retry strategy with 5-attempt limit and graceful failure handling
- **Automated Alerting System**: Two-tier Celery task system for real-time error/warning broadcasts with escape-safe HTML formatting
- **Maintenance Automation**: Cron-scheduled housekeeping tasks for database pruning and system optimization
- **Environment Standardization**: Schema-enforced configuration management preventing deployment inconsistencies

## Technology Stack
- **Backend**: Python 3.11, FastAPI, SQLAlchemy, PostgreSQL
- **Task Processing**: Celery, Redis
- **Messaging**: Telegram Bot API (python-telegram-bot)
- **DevOps**: Docker, GitHub Actions, DigitalOcean Container Registry
- **Configuration**: Environment-driven configuration with dtpyfw framework

## Impact & Results
- Unified log management across multiple microservices
- Automated incident response reducing manual monitoring overhead
- Scalable architecture supporting rapid service onboarding
- Production-ready system with full CI/CD automation and containerized deployment
