FROM node:15 as builder

WORKDIR /app

COPY package*.json ./
RUN npm install

COPY . .
RUN npm run build
#second stage
FROM nginx:alpine
RUN rm /etc/nginx/conf.d/default.conf
COPY nginx.conf /etc/nginx/conf.d/default.conf

WORKDIR /usr/share/nginx/html
RUN rm -rf ./*
COPY --from=builder /app/build .


EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]