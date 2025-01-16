FROM node:20 AS builder

WORKDIR /app

ENV API_URL=http://192.168.50.4:8087/api

COPY package*.json ./
RUN curl -I https://registry.npmjs.org
RUN npm install

COPY . .
RUN npm run build --prod

FROM nginx:alpine
COPY --from=builder /app/dist/frontend /usr/share/nginx/html

EXPOSE 4200
CMD ["nginx", "-g", "daemon off;"]
