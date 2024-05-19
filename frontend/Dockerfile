# Use Node.js as the base image
FROM node:alpine as builder

# Set the working directory in the container
WORKDIR /app

# Copy package.json and package-lock.json to the working directory
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the entire project to the working directory
COPY . .

# Build the React app for production
RUN npm run build

# Use Nginx as the base image for serving the static files
FROM nginx:alpine

# Copy the built app from the previous stage to the Nginx container
COPY --from=builder /app/build /usr/share/nginx/html

# Expose port 80
EXPOSE 80

# Start Nginx
CMD ["nginx", "-g", "daemon off;"]