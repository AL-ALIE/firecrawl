# Stage 1: Build the React application
FROM node:18-alpine AS build

# Set the working directory inside the container
WORKDIR /app

# Copy package.json and package-lock.json
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the rest of your application files
COPY . .

# Ensure the build directory exists before copying
RUN ls -la /app

# Build the React application
RUN npm run build

# Debug: Check if build directory exists
RUN ls -la /app/build

# Stage 2: Serve the React application using Node.js
FROM node:18-alpine AS production

# Set the working directory inside the container
WORKDIR /app

# Ensure the build directory exists before copying
RUN ls -la /app

# Copy the built React application from the previous stage
COPY --from=build /app/build ./build

# Install a simple static file server
RUN npm install -g serve

# Expose the port
EXPOSE 3003

# Start the application using "serve"
CMD ["serve", "-s", "build", "-l", "3003"]
