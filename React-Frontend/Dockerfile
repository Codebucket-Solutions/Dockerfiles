# Use the official Node.js image with the specified version
FROM node:14.15.1-buster-slim AS builder

# Install Git
RUN apt update && apt install git -y -qq

# Set the working directory inside the container
WORKDIR /app

# Copy package.json and package-lock.json to the working directory
COPY package*.json ./

# Use 'https' git
RUN git config --global url."https://".insteadOf git://

# Install dependencies
RUN npm install

# Copy all files from the current directory to the working directory
COPY . .

# Build the application
RUN npm run-script build

# Use the official Nginx image as the final base image
FROM nginx:latest

# Copy the build folder from the previous stage to Nginx's default public directory
COPY --from=builder /app/build /usr/share/nginx/html

# Expose port 80 to allow external access to the Nginx server
EXPOSE 80

# Nginx is started automatically by the base image, so no explicit CMD needed