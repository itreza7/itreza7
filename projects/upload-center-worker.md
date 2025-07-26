## Upload API Microservice

### Overview

A serverless asset management microservice providing secure file and photo upload and removal capabilities. Built on Cloudflare Workers and R2 storage, it exposes RESTful endpoints for client applications to stream, store, and delete binary assets—ensuring low-latency, globally distributed handling of user-generated content.

### Role & Responsibilities

* **Sole Backend Engineer**: Owned end-to-end design and implementation of the upload service.
* **API Design & Implementation**: Defined RESTful routes for health checks, home page, file/photo upload, and deletion.
* **Security & Access Control**: Developed middleware to enforce API key authentication on sensitive endpoints.
* **CI/CD Integration**: Configured GitHub Actions workflow for automated testing and deployment with Wrangler.

### Architecture & Design

* **Serverless Edge Runtime**: Leveraged Cloudflare Workers to run code at the network edge, minimizing request latency and scaling automatically.
* **Routing Layer**: Implemented a custom router utility to match HTTP methods and URL patterns, invoke middleware, parse request bodies, and format responses uniformly.
* **Middleware Pipeline**: Created an authorization middleware to validate API keys and respond with standard JSON error payloads on failure.
* **Storage Integration**:

  * **R2 Bucket**: Streams incoming binary data into a Cloudflare R2 bucket for generic file storage.
  * **Images API**: Proxies photo uploads to Cloudflare Images for optimized delivery, using multipart form-data and secure bearer tokens.
* **Utility Modules**: Centralized logic for request parsing, response creation, path normalization, and prefix manipulation to maximize code reuse and maintainability.
* **Error Handling & Observability**: Wrapped all fetch requests in try/catch, emitting structured logs for successful operations and catching unhandled exceptions with a standardized error message.

### Technologies Used

* **Languages & Runtimes**: JavaScript (ECMAScript Modules) on Cloudflare Workers.
* **Serverless Platform**: Wrangler CLI, Cloudflare Workers & R2, Cloudflare Images API.
* **Testing & QA**: Vitest with pool-worker support for edge-environment simulation.
* **CI/CD**: GitHub Actions for automated deploys on push to main, secure secret management for API credentials.
* **Version Control & Workflow**: Git, GitHub, branching strategy triggering on merges to main.

### Key Contributions & Solutions

* **Modular Router**: Abstracted HTTP routing into a reusable factory—handlers declare only method, path pattern, middlewares, and body/response modes.
* **Streamlined Upload Flow**: Handled large binary payloads by streaming form-data directly into R2, automatically inferring file extensions and content types.
* **Photo Optimization**: Integrated Cloudflare Images workflow by dynamically constructing multipart requests, extracting returned asset IDs, and generating CDN-ready URLs.
* **Unified Response Utility**: Developed a single function to standardize JSON responses (success flag, data/message), status codes, and caching headers.
* **Secrets Management in CI**: Automated secure injection of API\_KEY and CF\_IMAGE\_TOKEN into the Workers environment during GitHub Actions deploy.

### Challenges & Resolutions

* **Large File Handling**: Ensured memory-efficient streaming by directly writing formData arrayBuffers into R2, avoiding in-memory buffering.
* **Edge-Environment Testing**: Configured Vitest pool workers to replicate Cloudflare runtime for reliable local testing of edge-specific APIs.
* **Authentication Flow**: Designed a flexible middleware pipeline to support additional security or monitoring layers in the future without modifying core handlers.
* **Error Transparency**: Balanced user-friendly error messages with internal logging, so operational issues surface in observability dashboards without exposing internals.

### Outcome

Successfully delivered a fully automated, globally distributed upload service integrated into the broader application, powering client-side asset management with high throughput and robust security. The modular design and comprehensive test coverage ensure maintainability, extensibility, and resilience in production.
