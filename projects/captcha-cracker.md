# CAPTCHA Cracker Microservice

## Overview

A lightweight, containerized microservice that automatically solves image-based CAPTCHAs by fetching images from URLs, processing them with computer vision techniques, and returning decoded character strings. Designed for integration into automated workflows such as web testing, data extraction, and pipeline verification.

## Technical Architecture

### Microservice Design
- **RESTful API**: FastAPI application with asynchronous endpoints
- **Authentication**: API key-based security with dependency injection
- **Session Management**: HTTP session support with cookie handling
- **Containerization**: Docker-based deployment for consistent environments

### Image Processing Pipeline
- **Image Retrieval**: HTTP-based image fetching with session cookie support
- **Preprocessing**: Grayscale conversion using weighted dot-product filtering
- **Segmentation**: Dynamic sliding-window algorithm for character isolation
- **Adaptive Parameters**: Configurable window width for varying CAPTCHA formats

### Machine Learning Integration
- **Multi-Model Support**: Separate Keras models for 3-character and 4-character CAPTCHAs
- **Batch Inference**: Optimized prediction pipeline with segment resizing
- **Model Loading**: Warm-loaded models to minimize cold-start latency

## Technologies & Tools

- **Backend**: Python 3, FastAPI, TensorFlow/Keras
- **Computer Vision**: OpenCV, NumPy
- **HTTP Processing**: requests library with session management
- **Containerization**: Docker
- **API Security**: Header-based authentication

## Key Technical Achievements

### Dynamic Segmentation Algorithm
Developed a parameterized sliding-window segmentation system that adapts to varying CAPTCHA widths and character counts, reducing manual configuration for new formats.

### Performance Optimization
- Implemented batch processing for pre/post-processing operations
- Achieved real-time response times through optimized model loading
- Minimized Docker image size through dependency optimization

### Scalable Architecture
- Modular authentication system supporting future extensions (OAuth, JWT)
- Unified solver interface enabling seamless addition of new CAPTCHA types
- Container-ready deployment for cloud environments

## Technical Challenges Solved

### Image Quality Variability
- Implemented flexible filtering parameters for inconsistent CAPTCHA rendering
- Explored adaptive binarization techniques for noise reduction
- Added data augmentation (rotation, noise, contrast) to improve model robustness

### Performance vs. Accuracy Trade-offs
- Optimized sliding-window stride and segment width parameters
- Balanced character isolation accuracy with response time requirements
- Implemented efficient resource management in containerized environments

## Results & Impact

- Successfully processes both 3-character and 4-character CAPTCHAs with high accuracy
- Reduced manual intervention in automated workflows
- Delivered portable, production-ready solution with Docker containerization
- Demonstrated extensibility for future CAPTCHA format support
