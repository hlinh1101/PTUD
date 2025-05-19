FROM node:18-alpine
WORKDIR /app

# 1) Copy package và cài dependencies
COPY package*.json ./
RUN npm ci

# 2) Copy toàn bộ source
COPY . .

# 3) Đảm bảo prisma binary có quyền executable, rồi sinh Prisma Client
RUN chmod +x node_modules/.bin/prisma \
    && npx prisma generate

# 4) Expose và khởi chạy
EXPOSE 8000
CMD ["node", "-r", "ts-node/register", "src/index.ts"]
