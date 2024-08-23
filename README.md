# Table of Contents

- [LOCAL TESTING](#local-testing)
- [NEXT STEP](#next-step)
- [DIRECTORY STRUCTURE](#directory-structure)
- [OPERATIONS](#operations)

# STATUS

[![Build and Deploy Docker Image](https://github.com/Knowvus/Duke_rs/actions/workflows/deploy.yml/badge.svg)](https://github.com/Knowvus/Duke_rs/actions/workflows/deploy.yml)

# MILESTONES

[] Create_User Integrate with Postgres
   [] Error Message for Duplicate Email
[] Create_Task Integrate with Postgres
   [] Non Null String

these endpoints should be callable via CLI [this is how we can test since it's a microservice]
Call the endpoint on the server - server servces the DB, DB responses, server serves DB response

# LOCAL TESTING

    ```
    Build Time: ~4 Mins
    ```

1) **Run the Server Locally:**
    ```
    cargo clean
    cargo build
    cargo run
    ```

2) **Endpints:**
    ```
    - curl http://localhost:8080/create_user -d "mkaminski1337@gmail.com"
    - curl http://localhost:8080/create_task -d "Reverse this String!"
    - curl -f http://localhost:8080/health
    - curl -f http://localhost:8080/docs
    ```
4) **Review Secrets:**
    ```
    infisical secrets --env=prod
    ```
    Other Environments
    ```
    staging
    dev
    ```

5) **API Documentation**
    ```
    OpenAPI JSON: http://<your-droplet-ip>:8080/api-doc/openapi.json
    Swagger UI: http://<your-droplet-ip>:8080/docs
    ```
    
6) **Docker Commands**
     ```
    docker ps -a
    docker ps
    docker inspect [service_name]
    docker logs [service_name]
    docker rm [container_id]
    ls
    ls -a
    sudo lsof -i :8080
    ```
7) **Swagger**
    ```
    curl -LO https://github.com/swagger-api/swagger-ui/archive/refs/heads/master.zip
    unzip master.zip
    ```
---

# TECHNICAL RESOURCES

## DIRECTORY STRUCTURE

```
src/
│
├── main.rs              # Entry point of the application
├── handlers/            # Directory for request handlers
│   ├── mod.rs           # Module file for the handlers
│   └── task.rs          # Task-related handler functions
│   └── user.rs          # User-related handler functions
├── schemas/             # Directory for schema definitions
│   ├── mod.rs           # Module file for the schemas
│   └── task.rs          # Schema for TaskBody
├── routes/              # Directory for route definitions
│   └── mod.rs           # Module file for routes
└── apidoc/              # Directory for OpenAPI documentation
    ├── mod.rs           # Module file for OpenAPI documentation
    └── openapi.rs       # Defines the OpenAPI schema using utoipa
```

## OPERATIONS

### `src/routes/`

**Purpose:** This folder contains all the route handlers that map API endpoints to their respective request handlers.

**Example:** `mod.rs` defines the route handling logic and integrates the handlers for `create_task` and `create_user`.

### `src/schemas/`

**Purpose:** This folder contains schema definitions used in your application and OpenAPI documentation.

**Example:** `task.rs` defines the `TaskBody` struct, which is used in the `create_task` handler and referenced in the OpenAPI documentation.

### `src/apidoc/`

**Purpose:** This folder is dedicated to OpenAPI documentation-related logic.

- **`mod.rs:`** This file exposes the OpenAPI documentation logic.
- **`openapi.rs:`** This file defines your OpenAPI schema using `utoipa`, pulling in schemas from the `schemas/` directory and paths from the `routes/` and `handlers/` directories to build the complete OpenAPI documentation.

### `src/utils/`

**Purpose:** This folder can store utility functions or modules that are shared across different parts of your application (e.g., error handling, logging, etc.).
