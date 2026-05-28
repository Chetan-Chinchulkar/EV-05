# Build stage
FROM node:18-alpine AS build

WORKDIR /app

# Copy package files
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy all files
COPY . .

# Build the application
RUN npm run build

# Runtime stage
FROM node:18-alpine

WORKDIR /app

# Install lightweight static file server
RUN npm install -g serve

# Copy built frontend assets
COPY --from=build /app/build ./build

EXPOSE 3000

CMD ["/bin/sh", "-c", "serve -s build -l ${PORT:-3000}"]