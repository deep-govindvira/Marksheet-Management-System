# Marksheet Management System - Frontend

This is the frontend application for the **Marksheet Management System**, built to manage student marks, departments, subjects, and results efficiently. The UI communicates with a backend REST API built using Spring Boot.

## Tech Stack

* React
* Axios (API calls)
* React Router (Routing)
* Tailwind CSS

## Getting Started

### 1. Clone the repository

```bash
git clone https://github.com/Industrial-Projects-2025-2026/fe-marksheet-processing.git
cd fe-marksheet-processing
```

---

### 2. Install dependencies

```bash
npm install
```
---

### 3. Configure Environment Variables

Create a `.env` file in the root directory:

```env
REACT_APP_SERVER_URL=https://mmsbe.arvrserver.co.in
PORT=3000 # spring boot backend endpoint
HOST=0.0.0.0
```

> Update the variables according to your backend server.

---

### 4. Run the application

```bash
npm start
```

The app will run on:

```
http://localhost:3000
```

## Build for Production

```bash
npm run build
```

## Running the Application with Docker

```bash
docker compose -p mms up
```

## Deployment of Frontend, Backend, ML part on EC2

```bash
git clone https://github.com/Industrial-Projects-2025-2026/fe-marksheet-processing.git

git clone https://github.com/Industrial-Projects-2025-2026/be-marksheet-processing.git

git clone https://github.com/Industrial-Projects-2025-2026/ml-marksheet-processing.git

# now create jar file for backend using mvnw clean package

mkdir mms

cd mms

mkdir be-marksheet-processing

mkdir be-marksheet-processing/target

mkdir fe-marksheet-processing

mkdir ml-marksheet-processing

cp  -r \
../be-marksheet-processing/.env \
../be-marksheet-processing/Dockerfile \
be-marksheet-processing/

cp  -r \
../be-marksheet-processing/target/backend-0.0.1-SNAPSHOT.jar \
be-marksheet-processing/target/

cp -r \
../fe-marksheet-processing/.env \
../fe-marksheet-processing/Dockerfile \
../fe-marksheet-processing/src \
../fe-marksheet-processing/public \
../fe-marksheet-processing/nginx.conf \
../fe-marksheet-processing/tailwind.config.js \
../fe-marksheet-processing/package-lock.json \
../fe-marksheet-processing/package.json \
fe-marksheet-processing/

cp -r \
../ml-marksheet-processing/.env \
../ml-marksheet-processing/Dockerfile \
../ml-marksheet-processing/api.py \
../ml-marksheet-processing/traineddata \
../ml-marksheet-processing/config.yaml \
../ml-marksheet-processing/requirements.txt \
ml-marksheet-processing/
```

Create single docker-compose.yaml file.
```yaml
version: '3.8'

services:

  nginx:
    image: nginx:alpine
    container_name: mms-nginx
    ports:
      - "80:80"
      - "443:443"
    # volumes:
    #   - ./nginx.conf:/etc/nginx/nginx.conf
    #   - ./certs:/etc/nginx/certs
    volumes:
      - ./nginx.conf:/etc/nginx/nginx.conf
      - /etc/letsencrypt:/etc/letsencrypt
    depends_on:
      - mms-frontend
      - mms-backend
      - mms-ml
    # restart: unless-stopped
    networks:
      - mms-network

  mms-frontend:
    container_name: mms-frontend
    build:
      context: ./fe-marksheet-processing
      dockerfile: Dockerfile
      args:
        REACT_APP_SERVER_URL: ${REACT_APP_SERVER_URL}
    image: mms-frontend:latest
    env_file:
      - ./fe-marksheet-processing/.env
    expose:
      - "3000"
    # restart: unless-stopped
    networks:
      - mms-network

  mms-backend:
    container_name: mms-backend
    build:
      context: ./be-marksheet-processing
      dockerfile: Dockerfile
    image: mms-backend:latest
    env_file:
      - ./be-marksheet-processing/.env
    environment:
      SPRING_DATASOURCE_URL: jdbc:postgresql://postgres-db:5432/postgres
      SPRING_DATASOURCE_USERNAME: postgres
      SPRING_DATASOURCE_PASSWORD: postgres
    expose:
      - "8080"
    depends_on:
      postgres:
        condition: service_healthy
    # restart: unless-stopped
    networks:
      - mms-network

  mms-ml:
    container_name: mms-ml
    build:
      context: ./ml-marksheet-processing
      dockerfile: Dockerfile
    image: mms-ml:latest
    env_file:
      - ./ml-marksheet-processing/.env
    expose:
      - "8000"
    # restart: unless-stopped
    networks:
      - mms-network

  postgres:
    image: postgres:16
    container_name: postgres-db
    environment:
      POSTGRES_DB: postgres
      POSTGRES_USER: postgres
      POSTGRES_PASSWORD: postgres
    volumes:
      - postgres_data:/var/lib/postgresql/data
    expose:
      - "5432"
    # restart: unless-stopped
    networks:
      - mms-network
    healthcheck:
      test: ["CMD-SHELL", "pg_isready -U postgres"]
      interval: 5s
      timeout: 5s
      retries: 10

  adminer:
    image: adminer
    container_name: adminer
    ports:
      - "8081:8080"
    depends_on:
      postgres:
        condition: service_healthy
    # restart: unless-stopped
    networks:
      - mms-network

  s3:
    image: minio/minio:latest
    container_name: local-s3
    command: server /data --console-address ":9001"
    environment:
      MINIO_ROOT_USER: admin
      MINIO_ROOT_PASSWORD: admin123
    ports:
      - "9000:9000"
      - "9001:9001"
    volumes:
      - s3_data:/data
    # restart: unless-stopped
    networks:
      - mms-network

volumes:
  postgres_data:
  s3_data:

networks:
  mms-network:
    name: mms-network
    driver: bridge
```

Create single nginx.conf
```conf
events {}

http {

  client_max_body_size 200M;

  server {
      listen 80;

      server_name mms.arvrserver.co.in
                  mmsbe.arvrserver.co.in
                  mmsml.arvrserver.co.in;

      return 301 https://$host$request_uri;
  }

  server {
      listen 443 ssl;

      server_name mms.arvrserver.co.in;

      ssl_certificate /etc/letsencrypt/live/mms.arvrserver.co.in/fullchain.pem;
      ssl_certificate_key /etc/letsencrypt/live/mms.arvrserver.co.in/privkey.pem;

      location / {
          proxy_pass http://mms-frontend:3000;
      }
  }

  server {
      listen 443 ssl;

      server_name mmsbe.arvrserver.co.in;

      ssl_certificate /etc/letsencrypt/live/mms.arvrserver.co.in/fullchain.pem;
      ssl_certificate_key /etc/letsencrypt/live/mms.arvrserver.co.in/privkey.pem;

      location / {
        proxy_pass http://mms-backend:8080;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
      }

      location /api/stream {
        proxy_pass http://mms-backend:8080;
        proxy_http_version 1.1;
        # prevent buffering (CRITICAL for SSE)
        proxy_buffering off;
        proxy_cache off;
        gzip off;

        # keep connection alive
        proxy_set_header Connection '';
        # forward auth header (IMPORTANT for your case)
        proxy_set_header Authorization $http_authorization;

        # SSE stability
        proxy_set_header X-Accel-Buffering no;
      }

  }

  server {
      listen 443 ssl;

      server_name mmsml.arvrserver.co.in;

      ssl_certificate /etc/letsencrypt/live/mms.arvrserver.co.in/fullchain.pem;
      ssl_certificate_key /etc/letsencrypt/live/mms.arvrserver.co.in/privkey.pem;

      location / {
          proxy_pass http://mms-ml:8000;
      }
  }

}
```

## At the end folder structure will look like this.
```bash
Desktop/
mms/
│
├── be-marksheet-processing/
│   ├── Dockerfile
│   ├── .env
│   └── target/
│       └── backend-0.0.1-SNAPSHOT.jar
│ 
├── fe-marksheet-processing/
│   ├── Dockerfile
│   ├── .env
│   └── other files
│
├── ml-marksheet-processing/
│   ├── Dockerfile
│   ├── .env
│   ├── api.py
│   ├── config.yaml
│   ├── requirements.txt
│   └── traineddata/
│ 
├── docker-compose.yml   
├── nginx.conf 
```

## Create zip of `mms` folder
## Upload to EC2
## Unzip on EC2
## Create Certificate on EC2

```bash
sudo certbot certonly --standalone \
-d mms.arvrserver.co.in \
-d mmsbe.arvrserver.co.in \
-d mmsml.arvrserver.co.in
```

# Run app
```bash
docker compose up -d
```