FROM node:18-alpine

WORKDIR /app

# Cài prisma CLI (global hoặc dev)
RUN npm install -g prisma

# Copy package files & cài đặt
COPY package*.json ./
RUN npm install

# Copy toàn bộ mã nguồn
COPY . .

# ✅ Cấp quyền thực thi nếu cần (nếu bạn dùng local CLI)
# RUN chmod +x ./node_modules/.bin/prisma

# Generate Prisma Client
RUN prisma generate

EXPOSE 8000

CMD ["npm", "run", "dev"]
