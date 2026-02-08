 # Stage 1: build & test
FROM node:21 AS backend-builder
WORKDIR /app

# Install dependencies first for caching
COPY package*.json ./
RUN npm ci

# Copy rest of the code
COPY . .

# Run tests (no watch mode!)
RUN npm run test

# Stage 2: production
FROM node:21-slim
WORKDIR /app
COPY --from=backend-builder /app ./
COPY .env.docker .env
EXPOSE 8080
CMD ["npm", "start"]
