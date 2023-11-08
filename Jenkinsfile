# Use an official Nginx runtime as the base image
FROM nginx:latest

# Set the working directory inside the container
WORKDIR /usr/share/nginx/html

# Copy your HTML and CSS files into the container
COPY . /usr/share/nginx/html

# Expose port 80 (the default HTTP port)
EXPOSE 80

# Start the Nginx web server when the container is run
CMD ["nginx", "-g", "daemon off;"]

