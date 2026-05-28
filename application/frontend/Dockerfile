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
FROM nginx:alpine

# Copy build files
COPY --from=build /app/build /usr/share/nginx/html

# Copy nginx template configuration (PORT is injected at runtime)
COPY nginx.conf /etc/nginx/templates/default.conf.template

EXPOSE 8080

CMD ["/bin/sh", "-c", "envsubst '${PORT}' < /etc/nginx/templates/default.conf.template > /etc/nginx/conf.d/default.conf && nginx -g 'daemon off;'"]