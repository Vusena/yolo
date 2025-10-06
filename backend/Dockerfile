# 🏗️ Build Stage
FROM node:18-alpine AS build

# Set working directory
WORKDIR /usr/src/app

# Install dependencies
COPY package*.json ./
RUN npm ci --production

# Copy application code
COPY . .

# 🧼 Production Stage
FROM node:18-alpine AS production

# Set working directory
WORKDIR /app

# Copy built app from build stage
COPY --from=build /usr/src/app /app

# Expose backend port
EXPOSE 5000

# Start the server
CMD ["node", "server.js"]
