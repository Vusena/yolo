FROM node:18-alpine AS build
WORKDIR /app
COPY package*.json ./
RUN npm ci --only=production
COPY . .

# Production image
FROM alpine:3.20
WORKDIR /app
RUN apk add --no-cache nodejs
COPY --from=build /app /app

EXPOSE 5000
CMD ["node", "server.js"]
