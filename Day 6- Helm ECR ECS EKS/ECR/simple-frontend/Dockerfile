# === STAGE 1: Build the React App ===
# Use an official Node.js image as the base for our build environment.
FROM node:18-alpine AS build

# Set the working directory inside the container.
WORKDIR /app

# Copy the package.json and package-lock.json files.
COPY package*.json ./

# Install the project dependencies.
RUN npm install

# Copy the rest of the application source code.
COPY . .

# Build the application for production.
RUN npm run build

# === STAGE 2: Serve the App with Nginx ===
# Use a lightweight Nginx image as the base for our final image.
FROM nginx:1.23-alpine

# Copy the built static files from the 'build' stage to Nginx's web root directory.
COPY --from=build /app/dist /usr/share/nginx/html

# Expose port 80 to allow traffic to the Nginx server.
EXPOSE 80

# The default Nginx command will start the server.
# This is the command that runs when the container starts.
CMD ["nginx", "-g", "daemon off;"]
