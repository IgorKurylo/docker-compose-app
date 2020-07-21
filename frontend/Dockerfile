FROM node:alpine as builder

WORKDIR /app

COPY package*.json ./

RUN npm install

COPY . .

ARG config

RUN npm run build

FROM nginx:alpine
RUN rm -rf /usr/share/nginx/html/*
COPY nginx.conf /etc/nginx/nginx.conf
COPY --from=builder /app/dist/out /usr/share/nginx/html
CMD ["nginx", "-g", "daemon off;"]
