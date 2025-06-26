# Reverse Proxy with NGINX and Microservices
This project demonstrates a simple microservice architecture using Docker Compose, with two backend services (`service1`, `service2`) and an NGINX reverse proxy to route traffic to them.

## 🚀 Setup Instructions

1. **Clone the repository:**
git clone https://github.com/your-username/your-repo-name.git
cd your-repo-name

2. Build and run the services with Docker Compose:
    docker-compose up --build

3. Access services via NGINX:
    http://localhost:8080/service1/ping
    http://localhost:8080/service2/ping

🔁 How Routing Works
NGINX is used as a reverse proxy that listens on port 8080. Based on the path in the URL, it routes the request to the appropriate service:
      /service1/* → forwards to service1:8001
      /service2/* → forwards to service2:8002

The routing is defined in nginx.conf like so:
------
location /service1/ {
    proxy_pass http://service1:8001/;
}

location /service2/ {
    proxy_pass http://service2:8002/;
}
-------

🎁 Bonus Features added:
1.Health Checks: Each service has a Docker health check using the /ping endpoint to ensure the container is healthy.
2.Logging: You can check routing and container logs using:
      docker-compose logs nginx
      docker-compose logs service1
      docker-compose logs service2
3.Clean and modular Docker setup

Status
 ✅ Service 1 reachable through NGINX
 ✅ Service 2 reachable through NGINX
 ✅ Health checks configured
