FROM node:20-alpine

WORKDIR /app

# Cài Prisma CLI
RUN npm install -g prisma

# Copy và cài dependency
COPY package*.json ./
RUN npm install

# Copy source code
COPY . .

# Tạo Prisma Client
RUN prisma generate

EXPOSE 8000

# Chạy production command
CMD ["npm", "start"]
