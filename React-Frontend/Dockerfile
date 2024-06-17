# Use the official Node.js image with the specified version
FROM node:16.14.0-stretch-slim AS builder

# Install Git
RUN apt update && apt install git -y -qq

# Set the working directory inside the container
WORKDIR /app

# Copy package.json and package-lock.json to the working directory
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy all files from the current directory to the working directory
COPY . .

# Build the application
RUN npm run-script build

# Use the official Nginx image as the final base image
FROM nginx:latest

# Download nginx.conf using curl and place it in /etc/nginx/conf.d/
RUN curl -o /etc/nginx/conf.d/default.conf https://minio.internal.codebuckets.in/minio/ui/public-tools-config/nginx/react/nginx.conf

# Copy the build folder from the previous stage to Nginx's default public directory
COPY --from=builder /app/build /usr/share/nginx/html

# Expose port 80 to allow external access to the Nginx server
EXPOSE 80

# Nginx is started automatically by the base image, so no explicit CMD needed
