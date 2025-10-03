# backend/Dockerfile

# 1. Use Node.js v18 on Alpine Linux as the base image
FROM node:24-alpine

# 2. Set working directory inside the container
WORKDIR /app

# 3. Copy package.json and package-lock.json, then install only production dependencies
COPY package*.json ./
RUN npm ci --production

# 4. Copy the rest of the backend code (server.js, routes, models, etc.)
COPY . .

# 5. Expose backend API port
EXPOSE 5000

# 6. Start the backend server
CMD ["node", "server.js"]
# Temporary change to test Git tracking
