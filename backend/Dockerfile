FROM node:18-alpine

WORKDIR /app

# 1) Cài prisma, ts-node và typescript globally
RUN npm install -g prisma ts-node typescript

# 2) Copy và cài dependencies
COPY package*.json ./
RUN npm install

# 3) Copy source
COPY . .

# 4) Sinh Prisma Client
RUN chmod +x ./node_modules/.bin/prisma && npx prisma generate

# 5) Expose
EXPOSE 8000

# 6) Chạy TS trực tiếp bằng ts-node/register
CMD ["node", "-r", "ts-node/register", "src/index.ts"]
