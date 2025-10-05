# Build Stage
FROM node:18-alpine AS build

WORKDIR /app

# Install required system packages for crypto support
RUN apk update && apk add --no-cache openssl ca-certificates

# Set env to use legacy OpenSSL provider
ENV NODE_OPTIONS=--openssl-legacy-provider

# Copy package files and install dependencies
COPY package*.json ./
RUN npm install

# Copy source code
COPY . .

# Build the React app
RUN npm run build

# Production Stage
FROM nginx:stable-alpine AS production
COPY --from=build /app/build /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
