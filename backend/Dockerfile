# backend/Dockerfile
FROM node:18-alpine

WORKDIR /app

# 1) Cài dependencies
COPY package*.json ./
RUN npm install

# 2) Copy toàn bộ source
COPY . .

# 3) Sinh Prisma Client (vẫn giữ bước này nếu bạn dùng Prisma)
RUN chmod +x ./node_modules/.bin/prisma && npx prisma generate

# 4) Ép ts-node biên dịch TS → CJS để tránh ERR_REQUIRE_CYCLE_MODULE
ENV TS_NODE_COMPILER_OPTIONS='{"module":"commonjs"}'

# 5) Expose port
EXPOSE 8000

# 6) Chạy file TS qua ts-node/register (không cần sửa package.json)
CMD ["node", "-r", "ts-node/register", "src/index.ts"]
