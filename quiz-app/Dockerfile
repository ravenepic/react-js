# Stage 1: Build
FROM node:18 AS builder

WORKDIR /app

# Only copy package files first to leverage caching
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy source files
COPY . .

# Build the app
RUN npm run build

# Stage 2: Production image
FROM node:18-alpine AS production

WORKDIR /app

# Copy only necessary files from builder
COPY --from=builder /app/package*.json ./
COPY --from=builder /app/node_modules ./node_modules
COPY --from=builder /app/dist ./dist

# Expose port and run
EXPOSE 8080
CMD ["npm", "run", "start"]
