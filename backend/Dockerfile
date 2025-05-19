FROM node:18-alpine
WORKDIR /app

# 1) Copy file để cài cả dependencies và devDependencies
COPY package*.json ./
# Bỏ npm ci --omit=dev; chỉ dùng npm ci (mặc định cài devDependencies khi NODE_ENV!=production)
RUN npm ci

# 2) Copy source
COPY . .

# 3) Khôi phục exec-bit và generate Prisma
RUN chmod +x node_modules/.bin/prisma \
    && npx prisma generate

EXPOSE 8000

# 4) Chạy bằng npx để đảm bảo ts-node luôn dùng bản cục bộ
CMD ["npx", "ts-node", "src/index.ts"]
