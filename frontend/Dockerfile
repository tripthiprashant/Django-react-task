# Stage 1: Build React application
FROM node:20-bullseye AS build

WORKDIR /app

# Compatibility for older Webpack/react-scripts
ENV NODE_OPTIONS=--openssl-legacy-provider

COPY package*.json ./

RUN npm ci

COPY . .

RUN npm run build


# Stage 2: Serve React using Nginx
FROM nginx:alpine

COPY --from=build /app/build /usr/share/nginx/html

COPY nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
