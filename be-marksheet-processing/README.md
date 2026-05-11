# Marksheet Management System - Backend

This repository contains the backend implementation of the Marksheet Management System built using **Spring Boot**. The
system manages student marks, boards, departments, and related academic data with secure APIs.

## Tech Stack

* Java 21+
* Spring Boot
* Spring Data JPA (Hibernate)
* Spring Security + JWT
* PostgreSQL (or MySQL)
* Flyway
* Maven
* Lombok

## Getting Started

### 1. Clone the repository

```bash
git clone https://github.com/Industrial-Projects-2025-2026/be-marksheet-processing
cd be-marksheet-processing
```

---

### 2. Configure Environment Variables

Create a .env file in the root directory:

```env
SPRING_APPLICATION_NAME=backend
SPRING_SERVLET_MULTIPART_MAX_FILE_SIZE=50MB
SPRING_SERVLET_MULTIPART_MAX_REQUEST_SIZE=1GB
SERVER_PORT=8080
SPRING_THREADS_VIRTUAL_ENABLED=true

SPRING_DATASOURCE_URL=jdbc:postgresql://postgres-db:5432/postgres
SPRING_DATASOURCE_USERNAME=postgres
SPRING_DATASOURCE_PASSWORD=postgres
SPRING_DATASOURCE_DRIVER_CLASS_NAME=org.postgresql.Driver

SPRING_JPA_HIBERNATE_DDL_AUTO=none
SPRING_JPA_SHOW_SQL=false
SPRING_JPA_PROPERTIES_HIBERNATE_FORMAT_SQL=true

SPRING_FLYWAY_ENABLED=true
SPRING_FLYWAY_BASELINE_ON_MIGRATE=true
SPRING_FLYWAY_CLEAN_DISABLED=true
SPRING_FLYWAY_OUT_OF_ORDER=false
SPRING_FLYWAY_LOCATIONS=classpath:db/migration

SPRING_MAIL_HOST=smtp.gmail.com
SPRING_MAIL_PORT=587
SPRING_MAIL_USERNAME=sample@gmail.com
SPRING_MAIL_PASSWORD=abcd efgh ijkl mnop

SPRING_JWT_SECRET=your-256-bit-secret-key-change-this
SPRING_JWT_ACCESS_EXPIRATION=900000        # 15 minutes
SPRING_JWT_REFRESH_EXPIRATION=604800000    # 7 day

SPRING_ALLOWED_ORIGIN=https://mms.arvrserver.co.in

# Please ignore since files are stored in s3. But don't comment.
UPLOAD_PATH=/Desktop/user/uploads # where you want to store uploaded files

NO_OF_THREADS=16 # At a time how many files to process.

PROCESS_API_URL=http://mms-ml:8000/process
S3_ENDPOINT_URL=http://s3:9000
S3_ACCESS_KEY=admin
S3_SECRET_KEY=admin123
S3_REGION=us-east-1
S3_BUCKET=marksheets
```

> Please update the variables based on your database server configuration and add the file path in the “Environment
> Variables” section in IntelliJ.

---

### 4. Build the Project

```bash
./mvnw clean install
```

---

### 5. Run the Application

```bash
./mvnw spring-boot:run
```

Application will start at:

```
http://localhost:8080
```

## Build for Production

```bash
./mvnw clean package
```

## Running the Application with Docker

```bash
docker compose -p mms up
```

## Local Database Setup (PostgreSQL with Docker)

Before running the backend, start PostgreSQL using Docker.

---

### `postgres-db.yaml`

```yaml
version: '3.8'

services:
  postgres:
    image: postgres:16
    container_name: postgres-db
    environment:
      POSTGRES_DB: postgres
      POSTGRES_USER: postgres
      POSTGRES_PASSWORD: postgres
    ports:
      - "5432:5432"
    volumes:
      - postgres_data:/var/lib/postgresql/data
    restart: unless-stopped

  # UI for DB
  adminer:
    image: adminer
    container_name: adminer
    ports:
      - "8081:8080"
    depends_on:
      - postgres
    restart: unless-stopped

  # ER diagram generator (CLI only)
  schemaspy:
    image: schemaspy/schemaspy:latest
    container_name: schemaspy
    command: >
      -t pgsql
      -host postgres
      -port 5432
      -db postgres
      -u postgres
      -p postgres
    volumes:
      - ./er-output:/output
    depends_on:
      - postgres
    profiles:
      - er

volumes:
  postgres_data:

# docker-compose -f postgres-db.yaml -p mms up -d
# docker compose -f postgres-db.yaml -p mms --profile er run --rm schemaspy
```

## Local S3 Storage Setup (MinIO)

The system uses S3-compatible storage for file uploads.  
For local development, **MinIO** is used as the S3 provider.

---

### `s3.yaml`

```yaml
services:
  s3:
    image: minio/minio:latest
    container_name: local-s3
    command: server /data --console-address ":9001"
    ports:
      - "9000:9000"   # S3 API
      - "9001:9001"   # Web Console
    environment:
      MINIO_ROOT_USER: admin
      MINIO_ROOT_PASSWORD: admin123
    volumes:
      - s3_data:/data

volumes:
  s3_data:

# docker compose -f s3.yaml -p mms up -d
```