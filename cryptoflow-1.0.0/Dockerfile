# Build stage
FROM node:20.13.1-alpine AS builder
WORKDIR /app

COPY package*.json ./
RUN npm ci

COPY . .
RUN npm run build

# Runtime stage - use Nginx for serving static files
FROM nginx:stable-alpine
WORKDIR /usr/share/nginx/html

# remove default nginx static files
RUN rm -rf ./*

# copy only the production build
COPY --from=builder /app/build ./

EXPOSE 8080
CMD ["nginx", "-g", "daemon off;"]
