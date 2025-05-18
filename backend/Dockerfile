FROM node:20-alpine

WORKDIR /app

# Cài Prisma + ts-node/TypeScript globally
RUN npm install -g prisma ts-node typescript

# Copy và cài dependencies
COPY package*.json ./
RUN npm install

# Copy source
COPY . .

# Generate Prisma Client
RUN prisma generate

EXPOSE 8000

# Thay đổi entrypoint: không cần sửa package.json
# Chạy file TS bằng ts-node mà không cần script "start"
CMD ["node", "-r", "ts-node/register", "src/index.ts"]
