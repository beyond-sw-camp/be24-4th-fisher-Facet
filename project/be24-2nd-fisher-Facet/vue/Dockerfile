FROM node:24.12.0-slim AS builder
WORKDIR /app

COPY package.json ./
COPY ./  ./

RUN npm install
RUN npm run build

# 실행 단계
FROM nginx:alpine
COPY --from=builder /app/dist  /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]