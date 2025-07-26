# Automotive Website Data Scraper & Management System

## Project Overview

A scalable backend service designed to scrape, centralize, and expose dealer, vehicle, model, incentive, and brochure data from automotive websites. The microservice provides RESTful endpoints to ingest, query, and manage structured automotive information, enabling real-time data synchronization across applications.

## Technical Architecture

### System Design

- **Layered Architecture**: Configuration layer, data models, validation schemas, business controllers, API routing, and middleware
- **Design Patterns**: Dependency injection for database sessions, custom exception mapping, bulk operations optimization
- **Data Processing**: Web scraping capabilities with structured data extraction and normalization

### Core Components

- **Configuration**: Environment-aware settings loaded via typed configuration modules
- **Data Models**: Declarative ORM schema with InnoDB engine defaults and relationship mapping for one-to-many associations (dealers→vehicles, models→features)
- **Schemas**: Pydantic models for request validation and uniform response shaping
- **Controllers**: Encapsulated business logic for CRUD and bulk operations, handling JSON payloads and transactional consistency
- **Routing**: FastAPI routers grouping resources by domain (dealer, model, incentive, vehicle, brochure)
- **Middleware**: Global exception handling, request timing for observability, and standardized error responses

## Technology Stack

- **Backend**: Python 3.x, FastAPI, Starlette
- **Database**: MySQL with mysqlconnector, InnoDB engine defaults
- **ORM & Validation**: SQLAlchemy, Pydantic
- **Deployment**: uWSGI/uvicorn hosting with environment-based configuration
- **Supporting Libraries**: python-dotenv, dateutil for timestamp handling

## Key Technical Features

### Data Processing & Management

- **Robust Data Modeling**: Normalized table schemas with meta-configured table arguments, enabling efficient indexing and relationship cascades
- **Type-Safe API Contracts**: Pydantic schemas covering create, update, list, and detailed views with strict validation and clear API documentation
- **Bulk Operations**: Batch creation and clearing of brochure and incentive records to support high-volume data refresh workflows

### Performance & Security

- **Authentication System**: Bearer token validation and designated user-agent headers for secure endpoint access
- **Observability**: Middleware for request latency measurement and exception handling with standardized JSON error payloads
- **Database Optimization**: Bulk-update endpoints supporting batch ingestion of large payloads

## Technical Challenges & Solutions

### Complex Data Processing

- **Challenge**: Handling nested JSON fields from scraped data sources
- **Solution**: Created validation module to detect and parse JSON safely before database insertion

### Data Consistency

- **Challenge**: Maintaining accurate timestamp updates across related entities
- **Solution**: Orchestrated explicit session commits and targeted column updates within controller logic for `updated_at` and domain-specific timestamp fields

### Environment Management

- **Challenge**: Configuration consistency across development, staging, and production environments
- **Solution**: Implemented single settings module reducing configuration drift and streamlining CI/CD pipelines

## Project Outcomes

- Delivered production-ready microservice handling automotive data aggregation and management
- Achieved comprehensive API coverage with versioned contracts
- Established foundation for enhanced features including caching layers, analytics integration, and event streaming capabilities
- Enabled reliable real-time data access for automotive applications
