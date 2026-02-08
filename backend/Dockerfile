 # Stage 1: build & test
FROM node:21 AS backend-builder

WORKDIR /app

# Copy only package files first (caching layer)
COPY package*.json ./

# Install dependencies
RUN npm ci

# Copy the rest of the code
COPY . .

# Run tests (remove watch mode!)
RUN npm run test

# Stage 2: production image
FROM node:21-slim

WORKDIR /app

# Copy everything from builder
COPY --from=backend-builder /app ./

# Copy environment
COPY .env.docker .env

# Expose port
EXPOSE 8080

# Start app
CMD ["npm", "start"]
