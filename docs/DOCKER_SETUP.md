# Docker Deployment Guide

## Introduction
This guide provides an overview of how to set up Docker for the Procurement project, including Docker setup instructions, docker-compose configuration, Dockerfile examples for both the frontend and backend, deployment steps, production configurations, monitoring instructions, and troubleshooting tips.

## Docker Setup Instructions
1. Install Docker:
   - Download Docker from [Docker's official site](https://www.docker.com/get-started).
   - Follow the installation instructions for your operating system.
   
2. Verify the installation:
   ```bash
   docker --version
   ```

3. Install Docker Compose (if not included):
   - Using the following command:
   ```bash
   sudo curl -L "https://github.com/docker/compose/releases/latest/download/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
   sudo chmod +x /usr/local/bin/docker-compose
   ```
   
4. Check Docker Compose version:
   ```bash
   docker-compose --version
   ```

## Docker-Compose Configuration
Here is an example of a `docker-compose.yml` file for the Procurement application:

```yaml
version: "3.8"
services:
  frontend:
    build:
      context: ./frontend
      dockerfile: Dockerfile
    ports:
      - "3000:3000"
  backend:
    build:
      context: ./backend
      dockerfile: Dockerfile
    ports:
      - "8000:8000"
    environment:
      - DATABASE_URL=mysql://user:password@db:3306/procurement
    depends_on:
      - db
  db:
    image: mysql:latest
    environment:
      MYSQL_DATABASE: procurement
      MYSQL_ROOT_PASSWORD: password
    volumes:
      - db_data:/var/lib/mysql

volumes:
  db_data:
``` 

## Dockerfile Examples
### Frontend Dockerfile
```dockerfile
# Frontend Dockerfile
FROM node:14

WORKDIR /app
COPY . .

RUN npm install
RUN npm run build

CMD ["npm", "start"]
```

### Backend Dockerfile
```dockerfile
# Backend Dockerfile
FROM python:3.8

WORKDIR /app
COPY . .

RUN pip install -r requirements.txt

CMD ["python", "app.py"]
```

## Deployment Steps
1. Clone the repository:
   ```bash
   git clone https://github.com/Adrianlyle/Procurement.git
   cd Procurement
   ```

2. Build and run the containers:
   ```bash
   docker-compose up --build
   ```

3. Access the application:
   - Frontend: `http://localhost:3000`
   - Backend: `http://localhost:8000`

## Production Configurations
- Use a reverse proxy like Nginx for load balancing and securing connections.
- Ensure to configure environment variables for production, especially sensitive information such as API keys and database credentials.
- Use Docker volumes for persistent data storage.

## Monitoring Instructions
- Use monitoring tools like Prometheus or Grafana for tracking application performance.
- Consider implementing log aggregation with ELK stack (Elasticsearch, Logstash, Kibana).

## Troubleshooting Guide
- **Container won't start**: Check the logs using `docker-compose logs`.
- **Port conflicts**: Ensure the ports specified in the `docker-compose.yml` file are not already in use.
- **Database connection issues**: Verify database credentials and ensure the database service is up and running.

## Conclusion
This guide should help you set up and deploy the Procurement project using Docker effectively. For more detailed information, refer to the official Docker documentation.
