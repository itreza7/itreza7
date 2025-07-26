# Automated PostgreSQL Database Backup Service

## Project Overview

A containerized Python service that automates full backups of PostgreSQL databases, compresses dump files, and uploads them to Amazon S3. The solution runs on configurable schedules and ensures reliable, off-site preservation of database snapshots without manual intervention.

## Technical Architecture

### Core Components
- **Python Service**: Built on Python 3.9 with PostgreSQL client utilities and Supercronic for container-based scheduling
- **Configuration Management**: Environment-based configuration using python-dotenv for secure credential handling
- **Storage Layer**: AWS S3 integration for durable, scalable backup storage

### Backup Pipeline
1. **Database Discovery**: Automatically queries `pg_database` system catalog to identify all non-template databases
2. **Backup Process**: 
   - Executes `pg_dump` via subprocess for each database
   - Streams output directly into compressed gzip files
   - Uploads to S3 with structured naming: `<prefix>/<database>/<timestamp>.sql.gz`
3. **Cleanup**: Automatic removal of temporary files to prevent storage bloat

### Error Handling & Monitoring
- Comprehensive logging with configurable verbosity levels
- Graceful error handling that logs failures without stopping remaining backups
- Real-time log streaming to stdout for container log aggregation

## Technology Stack

### Core Technologies
- **Backend**: Python 3.9, psycopg2-binary, boto3, python-dotenv
- **Containerization**: Docker with python:3.9-slim base image
- **Scheduling**: Supercronic for reliable container-based cron jobs
- **Database Tools**: PostgreSQL pg_dump utility
- **Cloud Services**: AWS S3 for backup storage

### Deployment & Infrastructure
- Docker Compose for service orchestration
- Environment-driven configuration management
- CRON expression-based scheduling

## Key Technical Achievements

### Scalability & Automation
- **Dynamic Database Discovery**: Eliminates manual database listing through automated SQL queries
- **Flexible S3 Organization**: Implements hierarchical backup storage structure for easy retrieval
- **Zero-Configuration Scaling**: Automatically handles new databases without code changes

### Container Optimization
- **Efficient Scheduling**: Replaced traditional cron with Supercronic for proper container logging
- **Minimal Image Size**: Optimized Dockerfile with slim base image and selective package installation
- **Resource Management**: Atomic file operations with guaranteed cleanup

### Security & Reliability
- **Secure Credential Management**: Environment variable-based configuration without hardcoded secrets
- **Fault Tolerance**: Individual backup failures don't affect remaining operations
- **Temporary File Safety**: NamedTemporaryFile usage with explicit cleanup in all execution paths

## Technical Challenges Solved

### Container Logging
**Challenge**: Standard cron daemons don't output logs to stdout in containers  
**Solution**: Integrated Supercronic to stream logs directly to container output for monitoring

### Dynamic Database Management
**Challenge**: Manual database listing required updates for new databases  
**Solution**: Implemented PostgreSQL system catalog queries for automatic database discovery

### Large File Handling
**Challenge**: Atomic writes needed for large database dumps  
**Solution**: Used Python's NamedTemporaryFile with comprehensive error handling and cleanup

## Project Impact

- **Operational Efficiency**: Fully automated backup process requiring zero manual intervention
- **Data Resilience**: Reliable off-site backup storage with compression and organized retention
- **Deployment Simplicity**: Single Docker Compose command deployment across environments
- **Monitoring Integration**: Clear logging output for operational visibility and debugging

## Deployment

Single-command deployment using Docker Compose with environment-based configuration for seamless staging and production deployments.
