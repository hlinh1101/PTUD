FROM node:18-alpine
WORKDIR /app

# 1) Copy package và cài dependencies (bao gồm ts-node, typescript mới thêm)
COPY package*.json ./
RUN npm ci

# 2) Copy source
COPY . .

# 3) Sinh Prisma Client
RUN npx prisma generate

# 4) Expose port
EXPOSE 8000

# 5) Khởi chạy bằng ts-node (dùng local module)
CMD ["node", "-r", "ts-node/register", "src/index.ts"]
