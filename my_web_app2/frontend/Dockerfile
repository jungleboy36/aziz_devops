FROM node:16-alpine AS build
WORKDIR /usr/local/app
COPY package*.json /usr/local/app/
COPY . /usr/local/app/
RUN npm install
RUN npm run build
FROM nginx:alpine
# Remove the existing default.conf
RUN rm /etc/nginx/conf.d/default.conf
# Copy your custom Nginx configuration
COPY nginx.conf /etc/nginx/conf.d/
# Copy the build output from Stage 1 to Nginx's serve folder
COPY --from=build usr/local/app/dist/docker /usr/share/nginx/html
# Expose port 80 for external access
EXPOSE 80
# Start Nginx in the foreground
CMD ["nginx", "-g", "daemon off;"]

