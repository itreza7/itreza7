# Glasses Scraper - Multi-Brand Product Data Extraction Tool

## Project Overview

Python-based automation tool that extracts comprehensive product information (titles, colors, pricing, images, URLs) from multiple eyewear brand websites. Consolidates disparate site structures into standardized CSV reports for competitive analysis and inventory monitoring.

## Technical Architecture

**Modular Design Pattern**

- Shared helper module for HTTP session management, WebDriver configuration, and logging
- Brand-specific scraper modules with encapsulated extraction logic
- Centralized orchestrator script for resource management and execution flow

**Hybrid Scraping Approach**

- XML sitemap parsing for efficient URL discovery
- Selenium WebDriver automation for JavaScript-heavy content
- BeautifulSoup4 with lxml parser for high-performance HTML extraction
- HTTP session management with intelligent retry mechanisms

## Technology Stack

- **Python 3.x** - Core development language
- **Selenium WebDriver (Chrome)** - Browser automation for dynamic content
- **Requests & urllib3** - HTTP session management with retry strategies
- **BeautifulSoup4 & lxml** - HTML/XML parsing and data extraction
- **CSV** - Standardized data output format

## Key Technical Achievements

**Resilient Network Layer**

- Implemented exponential backoff retry mechanism for failed HTTP requests
- Built session management system to handle rate limiting and connection timeouts

**Dynamic Content Handling**

- Automated modal dialog detection and dismissal
- Implemented wait strategies for lazy-loaded content and asynchronous elements

**Scalable Architecture**

- Extensible module interface allowing new brand integrations with minimal code changes
- Abstracted common functionality into reusable components

**Error Recovery & Monitoring**

- Comprehensive exception handling with detailed logging
- Failed URL tracking with continuation logic for uninterrupted processing

## Technical Challenges Solved

- **Site Structure Variability**: Designed flexible CSS selector strategies adaptable to different HTML structures
- **Performance Optimization**: Balanced Selenium wait times with processing throughput requirements
- **Data Consistency**: Normalized diverse product data formats into unified CSV schema

## Project Impact

- Automated manual data collection processes across multiple brand websites
- Generated clean, standardized datasets for analytics and competitive intelligence
- Delivered maintainable codebase supporting rapid addition of new data sources
- Enabled real-time product catalog monitoring and pricing analysis
