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

# Debug: List files before build
RUN ls -la /app

# Build the React application (Vite outputs to `dist/`)
RUN npm run build

# Debug: Check if `dist/` folder exists
RUN ls -la /app/dist

# Stage 2: Serve the React application using Node.js
FROM node:18-alpine AS production

# Set the working directory inside the container
WORKDIR /app

# Copy the built React application from the previous stage
COPY --from=build /app/dist ./dist

# Install a simple static file server
RUN npm install -g serve

# Expose the port
EXPOSE 3003

# Start the application using "serve"
CMD ["serve", "-s", "dist", "-l", "3003"]
