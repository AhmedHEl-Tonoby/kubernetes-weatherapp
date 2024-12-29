# Weather App 🌦️

## Overview
The **Weather App** is a Kubernetes-based application designed to simulate a weather service system. The application consists of three interconnected **microservices**:  
1. **Authentication Service**  
2. **Weather Service (API)**  
3. **UI Service**  

The project uses Kubernetes to orchestrate deployments, manage configurations, and secure the system through TLS. It’s designed to be scalable, secure, and easy to use.

---

## Architecture

### Microservices
1. **Authentication Service**:
   - **Purpose**: Handles user authentication by storing credentials and managing access.
   - **Database**: Uses a MySQL database deployed as a **StatefulSet** for persistent storage.
   - **Connection**: Exposes an internal service to the backend for secure interactions.

2. **Weather Service (API)**:
   - **Purpose**: Provides weather data via APIs.
   - **Features**:
     - Fetches real-time or simulated weather data.
     - Responds to requests from the UI.
   - **Implementation**: Deployed as a **Deployment** with readiness and liveness probes.

3. **UI Service**:
   - **Purpose**: Displays a user-friendly interface for weather updates.
   - **Features**:
     - Responsive web interface.
     - Fetches data from the Weather API.
   - **Implementation**: Deployed as a **Deployment** and exposed through an **Ingress**.

---

## System Design
```plaintext
                +----------------------+
                |     User Browser     |
                +----------------------+
                        |
                        | HTTPS (TLS)
                        |
                  +-------------+
                  |    Ingress   |
                  +-------------+
                        |
          +-------------+-------------+
          |                           |
+--------------------+      +--------------------+
|        UI          |      |    Weather API     |
+--------------------+      +--------------------+
          |                           |
          +-------------+-------------+
                        |
                 +----------------+
                 | Authentication |
                 |   (MySQL DB)   |
                 +----------------+
