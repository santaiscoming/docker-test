# 빌드 스테이지
FROM node:18-alpine AS builder

WORKDIR /app

# 의존성 설치
COPY package.json ./
RUN npm install

# 소스 코드 복사
COPY . .

# 프로덕션용 빌드
RUN npm run build

# 실행 스테이지
FROM nginx:alpine

# nginx 설정 파일 복사
COPY nginx.conf /etc/nginx/conf.d/default.conf

# 빌드된 파일들을 nginx로 복사
COPY --from=builder /app/dist /usr/share/nginx/html

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"] 