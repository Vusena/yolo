
##  BACKEND CONTAINER
#  Comments one the choice of the base image on which to build the container.
The backend container uses node:18-alpine for both the build and production stages. Alpine Linux is preferred for its minimal footprint and security, while Node.js 18 provides long-term support and modern features. This combination ensures a lightweight, fast, and production-ready environment.

 # Dockerfile directives used

FROM node:18-alpine – Specifies the base image for the container.

WORKDIR /app – Sets the working directory inside the container to /app. All subsequent commands, like copying files or running scripts, will execute from this directory.

COPY package*.json ./ – Copies package.json and package-lock.json into the container. This allows installing dependencies without copying the entire source code first, which makes caching more effective.

RUN npm ci --production – Installs only production dependencies, keeping the image smaller and excluding development-only packages.

COPY . . – Copies all backend source files (server.js, routes/, models/, etc.) into the container.

FROM node:18-alpine AS production – Begins the final stage using the same base image.

COPY --from=build /usr/src/app /app – Transfers the built app into the production container.

EXPOSE 5000 – Documents the port that the backend service will listen on. This allows Docker or other services to know which port to map.

CMD ["node", "server.js"] – Sets the default command to run the backend server when the container starts.

# The backend image pushed to DockerHub as shown below
![backendyolo image](client/public/yolobackend-mage.png)


## CLIENT CONTAINER
#  Comments one the choice of the base image on which to build the container.
The client container uses two lightweight, production-grade base images to optimize both build and deployment:
node:18-alpine is used during the build stage. It’s chosen for its minimal size, fast performance, and compatibility with modern Node.js. This image provides a clean environment for installing dependencies and compiling the React app.

nginx:stable-alpine is used in the production stage. It’s ideal for serving static files efficiently, and is known for being lightweight, secure, and widely adopted in frontend deployments.

 # Dockerfile directives used
FROM node:18-alpine AS build - Begins the build stage using Node.js on Alpine Linux.

WORKDIR /app - Sets the working directory inside the container to /app.

COPY package*.json ./ - Copies the package configuration files to prepare for dependency installation.

RUN npm install - Installs all required project dependencies.

COPY . . - Copies the entire application source code into the container.

RUN npm run build - Compiles the React app into an optimized production build

FROM nginx:stable-alpine AS production - Starts the production stage using Nginx to serve the built static files.

COPY --from=build /app/build /usr/share/nginx/html - Transfers the compiled React build from the Node.js stage into Nginx’s default web directory.

EXPOSE 80 - Opens port 80 to allow HTTP traffic.

CMD ["nginx", "-g", "daemon off;"] - Sets the default command to run Nginx in the foreground and serve the application.

 # The backend image pushed to DockerHub as shown below
![clientyolo image](client/public/yoloclient-image.png)

## DATABASE CONTAINER
#  Comments one the choice of the base image on which to build the container.
The MongoDB container uses debian:bookworm-slim as its base image. This choice balances stability, compatibility, and minimal size:
Debian is a widely supported and secure Linux distribution, ideal for production environments. The bookworm-slim variant strips out unnecessary components, reducing image size while retaining full package manager support. This base ensures compatibility with MongoDB’s official Debian packages and avoids Alpine-related build issues.

 # Dockerfile directives used
FROM debian:bookworm-slim - Begins with a minimal Debian image to keep the container lightweight and secure.

-Set environment variables
ENV MONGO_VERSION=8.0.5
ENV DEBIAN_FRONTEND=noninteractive
-Defines the MongoDB version and disables interactive prompts during package installation.

- Install dependencies required for MongoDB
RUN apt-get update && apt-get install -y \
    curl \
    gnupg \
    && curl -fsSL https://pgp.mongodb.com/server-8.0.asc | gpg --dearmor -o /usr/share/keyrings/mongodb.gpg \
    && echo "deb [signed-by=/usr/share/keyrings/mongodb.gpg] https://repo.mongodb.org/apt/debian bookworm/mongodb-org/8.0 main" \
        > /etc/apt/sources.list.d/mongodb-org.list \
    && apt-get update && apt-get install -y mongodb-org-server mongodb-org-shell \
    && apt-get clean && rm -rf /var/lib/apt/lists/*
--- installs MongoDB securely by:
                                Adding the official MongoDB GPG key
                                Registering the MongoDB repository
                                Installing only the server and shell components
                                Cleaning up to reduce image size

Expose default MongoDB port - EXPOSE 27017
Create a data directory
VOLUME ["/data/db"]
WORKDIR /data/db

CMD ["mongod", "--bind_ip_all"] - Runs the MongoDB daemon and binds it to all available IP addresses, allowing external access.

# The database image pushed to DockerHub as shown below
![mongo database image](client/public/yolo-dbv1.png)

## Compose Status
The docker-compose.yml has successfully launched the full microservice stack — React frontend, Node.js backend, and MongoDB database — each running in its own container. The application is now live and accessible, with added products persisting correctly in the database. This confirms that inter-service communication and data storage are functioning as expected.

At this stage:

The app is running smoothly, as shown in the attached screenshot
Product data persists across container restarts via the named volume
The MongoDB image is functional but still unoptimized — further slimming is planned
Build sections for client and backend will be added to streamline local development 

![application1](client/public/application1.png)

