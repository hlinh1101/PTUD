FROM node:20-alpine

WORKDIR /app

# Cài prisma, ts-node và typescript toàn cục
RUN npm install -g prisma ts-node typescript

# Copy package.json và cài dependencies
COPY package*.json ./
RUN npm install

# Copy toàn bộ source
COPY . .

# Sinh Prisma Client
RUN prisma generate

EXPOSE 8000

# DÙNG loader ESM của ts-node để chạy .ts trực tiếp
CMD ["node", "--loader", "ts-node/esm", "src/index.ts"]
