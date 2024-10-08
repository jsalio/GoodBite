### STAGE 1: Build ###
FROM node:18-alpine AS build
WORKDIR /usr/src/app

# Copy package.json and package-lock.json for dependency installation
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the rest of the Angular source code
COPY . .

# Build the Angular app for production
RUN npm run build --prod

### STAGE 2: Serve ###
FROM nginx:1.17.1-alpine

# Copy the custom nginx configuration file
COPY nginx.conf /etc/nginx/nginx.conf

# Copy the Angular build output to nginx's default html folder
COPY --from=build /usr/src/app/dist/storeui /usr/share/nginx/html

# Expose port 80
EXPOSE 80

# Start nginx
CMD ["nginx", "-g", "daemon off;"]
