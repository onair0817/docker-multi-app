FROM node:16-alpine as builder
WORKDIR /app
COPY ./package.json ./
RUN npm install
COPY . .
RUN npm run build

FROM nginx
# listen하고 있는 서버 포트 뚫기
EXPOSE 3000 
# 컨테이너 안에 있는 nginx 설정 파일에 덮어쓰기
COPY ./nginx/default.conf /etc/nginx/conf.d/default.conf
# 빌더 파일 복사하기
COPY --from=builder /app/build  /usr/share/nginx/html
