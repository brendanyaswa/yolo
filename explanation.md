# choice of base image used 
Backend: The base image used is node:14, a lightweight and stable official Node.js image, well-suited for running Node.js applications in containers. It ensures compatibility with most libraries and avoids bloat.

Client: Also uses node:14-slim because the React frontend relies on Node for running scripts like react-scripts start. It simplifies development and build consistency between both services.
The -slim tag reduces image size significantly by excluding unnecessary packages, which improves build time and runtime performance.

# Dockerfile Directives Used

FROM: Specifies the base image (node:14).

WORKDIR: Sets the working directory in the container (/usr/src/app).

COPY: Transfers package*.json for optimized layer caching before installing dependencies, then copies the rest of the app.

RUN npm install: Installs project dependencies.

EXPOSE: Indicates the container’s runtime port.

ENV HOST=0.0.0.0: Ensures the React app binds to the correct interface inside the container.

# Docker-Compose Networking

Each service (backend, client) is defined under docker-compose.yaml.

Port Allocation:

Client: "3000:3000" → local access via http://localhost:3000

Backend: "5000:5000" → local access via http://localhost:5000

Bridge Network: Docker Compose automatically creates a bridge network (yolo_yolo-net) allowing containers to talk to each other by service name (e.g., the client can call http://backend:5000).

# Volume Definition

have added the mongo db volume to persist the data .


#  Git Workflow Used

The workflow followed was:

Initialize Git repository.

Regular commits with descriptive messages.

Final push to GitHub with  Dockerfiles,  docker-compose.yaml included.

# Successful Running & Debugging Measures

Both containers successfully started using docker compose up --build.

Issues debugged:

Port not reachable: Fixed by binding to 0.0.0.0 in React and Express.

Authentication failure while pushing to DockerHub: Resolved by generating a personal access token and using it in docker login.

#  Good Docker Practices

Image Tags: Used version tags such as brendanyaswa/yolo-client:1.0.0 and brendanyaswa/yolo-backend:1.0.0 instead of latest for clarity and reproducibility.

Layer Caching: Installed dependencies before copying the full app to benefit from Docker layer caching.

Multi-stage builds (optional for production) can be added later to reduce image size.

# Screenshot of DockerHub

![alt text](<Screenshot from 2025-04-24 10-14-58-1-2.png>)
![alt text](<Screenshot from 2025-04-24 10-15-50.png>)