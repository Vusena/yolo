# Start from a small base image
FROM debian:bookworm-slim

# Set environment variables
ENV MONGO_VERSION=8.0.5
ENV DEBIAN_FRONTEND=noninteractive

# Install dependencies required for MongoDB
RUN apt-get update && apt-get install -y \
    curl \
    gnupg \
    && curl -fsSL https://pgp.mongodb.com/server-8.0.asc | gpg --dearmor -o /usr/share/keyrings/mongodb.gpg \
    && echo "deb [signed-by=/usr/share/keyrings/mongodb.gpg] https://repo.mongodb.org/apt/debian bookworm/mongodb-org/8.0 main" \
        > /etc/apt/sources.list.d/mongodb-org.list \
    && apt-get update && apt-get install -y mongodb-org-server mongodb-org-shell \
    && apt-get clean && rm -rf /var/lib/apt/lists/*

# Expose default MongoDB port
EXPOSE 27017

# Create a data directory
VOLUME ["/data/db"]
WORKDIR /data/db

# Start MongoDB
CMD ["mongod", "--bind_ip_all"]
