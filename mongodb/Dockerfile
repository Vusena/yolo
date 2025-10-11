FROM debian:bullseye-slim

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get install -y --no-install-recommends \
    curl \
    gnupg \
    ca-certificates \
    && curl -fsSL https://pgp.mongodb.com/server-6.0.asc | gpg --dearmor -o /usr/share/keyrings/mongodb.gpg \
    && echo "deb [signed-by=/usr/share/keyrings/mongodb.gpg] https://repo.mongodb.org/apt/debian bullseye/mongodb-org/6.0 main" \
        > /etc/apt/sources.list.d/mongodb-org.list \
    && apt-get update && apt-get install -y --no-install-recommends \
       mongodb-org-server \
       mongodb-org-shell \
    && apt-get purge -y --auto-remove curl gnupg \
    && apt-get clean && rm -rf /var/lib/apt/lists/*

EXPOSE 27017
VOLUME ["/data/db"]
WORKDIR /data/db

CMD ["mongod", "--bind_ip_all"]
