FROM node:20-alpine

WORKDIR /app

# Cài prisma CLI (global nếu cần)
RUN npm install -g prisma

# Copy package và cài đặt
COPY package*.json ./
RUN npm install

# Copy toàn bộ source
COPY . .

# Generate Prisma client
RUN prisma generate

# Build app (giả sử bạn có `build` script tạo ra dist/)
RUN npm run build

EXPOSE 8000

# Chạy file build (NodeJS)
CMD ["npm", "start"]
