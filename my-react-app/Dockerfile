 # Base Image
# FROM node:19-alpine
# #working directry
# WORKDIR /app
# #copy package.json to app directory
# COPY package.json .
# #npm install
# RUN npm install
# #copy all files
# COPY . .
# #port expose
# EXPOSE 3000

# #run the code

# CMD [ "npm","start" ]

# Stage 1: Build the React application
FROM node:19-alpine as build

# Set the working directory
WORKDIR /app

# Copy package.json and package-lock.json (or yarn.lock) to the working directory
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the rest of the application source code
COPY . .

# Build the React application for production
RUN npm run build

# Stage 2: Serve the built React application using nginx
FROM nginx:alpine

# Copy build files from the previous stage to the Nginx web server directory
COPY --from=build /app/build /usr/share/nginx/html

# Expose port 80 to the outside world
EXPOSE 80

# Command to run Nginx in the foreground
CMD ["nginx", "-g", "daemon off;"]

