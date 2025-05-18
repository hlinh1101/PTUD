FROM node:20-alpine

WORKDIR /app

# 1) Cài prisma CLI và ts-node, typescript globally
RUN npm install -g prisma ts-node typescript

# 2) Copy package và install dependencies
COPY package*.json ./
RUN npm install

# 3) Copy toàn bộ source
COPY . .

# 4) Generate Prisma Client
RUN prisma generate

# 5) Mở port
EXPOSE 8000

# 6) Chạy trực tiếp TS
CMD ["npm", "start"]
