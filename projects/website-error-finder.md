# Website Error Detection & Link Validation Tool

## Project Overview

A command-line web crawler that automatically detects broken links and missing resources (HTTP 404 errors) across multiple domains. Built with the Scrapy framework, the tool traverses HTML pages, images, scripts, and stylesheets to generate structured reports in timestamped JSON files, supporting proactive website maintenance and optimal user experience.

## Technical Architecture

### Core Components

* **Modular Scrapy Framework** with separated spiders, pipelines, middlewares, and settings
* **MainSpider Engine** for intelligent crawling and resource validation
* **Signal-Based Collection System** for real-time error aggregation
* **Report Management Pipeline** with historical data merging capabilities

### Crawling Strategy

* **Deep Link Discovery** following anchor tags within allowed domains
* **Resource Validation** checking images, scripts, stylesheets, and other assets
* **Domain Boundary Control** preventing infinite crawls while capturing external resource errors
* **Custom Error Handling** isolating HTTP 404 responses from other status codes

### Data Processing

* **Real-time Error Collection** using Scrapy's signal manager
* **Historical Data Merging** combining new findings with existing reports
* **Timestamped Report Generation** for audit trails and trend analysis
* **Graceful Error Recovery** handling corrupted or missing report files

## Technologies & Tools

* **Python 3.9+**: Core development language
* **Scrapy Framework**: High-performance asynchronous web crawling
* **urllib.parse**: URL normalization and domain validation
* **JSON**: Structured data output and report management
* **Standard Logging**: Real-time crawler monitoring and debugging

## Key Technical Features

### Intelligent Crawling

* **URL Resolution**: Reliable handling of relative and absolute URLs using `response.urljoin`
* **Domain Filtering**: Advanced `urlparse` implementation for boundary detection
* **Loop Prevention**: Callback-based external domain flagging to avoid infinite recursion
* **Resource Discovery**: Comprehensive asset checking across multiple content types

### Error Detection & Reporting

* **Custom Error Pipeline**: Scrapy `errback` mechanism for isolated 404 error handling
* **Signal-Based Architecture**: Decoupled item generation from file processing
* **Report Aggregation**: Safe JSON file operations with corruption recovery
* **Historical Tracking**: Merge capabilities for trend analysis and change detection

### System Reliability

* **Exception Handling**: Robust error recovery for file I/O operations
* **Configuration Management**: Simple domain and URL configuration system
* **Logging Integration**: Comprehensive monitoring and debugging capabilities
* **Modular Design**: Extensible architecture for custom validation rules

## Technical Challenges Solved

### URL Handling Complexity

* **Challenge**: Managing relative vs. absolute URLs across different domains
* **Solution**: Implemented robust URL resolution using Scrapy's `response.urljoin` method

### Crawl Scope Management

* **Challenge**: Preventing infinite crawls while capturing all relevant errors
* **Solution**: Developed callback-based domain flagging system with external link tracking

### Data Integrity

* **Challenge**: Handling corrupted or missing report files during merging
* **Solution**: Built graceful error recovery with JSON validation and backup creation

## Project Impact

* **Automated Quality Assurance**: Eliminated manual link checking processes
* **Proactive Maintenance**: Early detection of broken resources before user impact
* **Historical Analysis**: Trend tracking capabilities for website health monitoring
* **Scalable Solution**: Multi-domain support with configurable crawling parameters
* **Extensible Framework**: Modular design enabling custom validation rules

## Skills Demonstrated

* **Web Scraping**: Advanced Scrapy framework implementation with custom pipelines
* **Python Development**: Object-oriented design, error handling, and data processing
* **System Design**: Modular architecture with separation of concerns
* **Data Management**: JSON processing, file I/O, and data aggregation
* **Quality Assurance**: Automated testing frameworks and validation systems
* **Problem Solving**: Complex URL handling and crawl boundary management
