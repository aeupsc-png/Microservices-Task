# Skill Test 1: Node.js Microservices Containerization

## 1. Overview

This project containerizes four Node.js microservices using Docker and Docker Compose.

## 2. Services and Ports

| Service | Port |
|---|---:|
| User Service | 3000 |
| Product Service | 3001 |
| Order Service | 3002 |
| Gateway Service | 3003 |

## 3. Prerequisites

- Docker Desktop installed and running
- Docker Compose available through the Docker CLI
- Ports 3000, 3001, 3002 and 3003 available

## 4. Start the Application

Run these commands from the directory containing this README:

    docker compose up --build -d
    docker compose ps
    docker compose logs --tail=50

## 5. Test the Endpoints

| Purpose | URL |
|---|---|
| User health | http://localhost:3000/health |
| List users | http://localhost:3000/users |
| Product health | http://localhost:3001/health |
| List products | http://localhost:3001/products |
| Order health | http://localhost:3002/health |
| List orders | http://localhost:3002/orders |
| Gateway health | http://localhost:3003/health |
| Gateway users | http://localhost:3003/api/users |
| Gateway products | http://localhost:3003/api/products |
| Gateway orders | http://localhost:3003/api/orders |

You can test these URLs in a browser or use PowerShell Invoke-RestMethod.

## 6. Create an Order Through the Gateway

Run:

    $body = @{ userId = 1; productId = 1 } | ConvertTo-Json
    Invoke-RestMethod -Uri "http://localhost:3003/api/orders" -Method Post -ContentType "application/json" -Body $body

The response should contain the created order details if the request succeeds.

## 7. Docker Network

All four services connect to the shared Docker bridge network named microservices-net. The gateway communicates with backend services using their Docker Compose service names.

## 8. Troubleshooting

- Start Docker Desktop if the Docker engine is unavailable.
- Run docker compose ps to inspect container status.
- Run docker compose logs --tail=100 to investigate errors.
- Check for port conflicts if a container cannot bind to a host port.
- Use service names, rather than localhost, for communication between containers.
- depends_on controls startup order but does not guarantee that a service is ready to accept requests.

## 9. Screenshots

Place genuine screenshots in the screenshots folder showing:
- All four containers running
- Successful service endpoint tests
- Successful gateway endpoint tests

## 10. GitHub Repository

https://github.com/aeupsc-png/Microservices-Task
