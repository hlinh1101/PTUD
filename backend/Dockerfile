FROM node:20-alpine

WORKDIR /app

# Copy package.json và package-lock.json
COPY package*.json ./

# Cài đặt dependencies (bao gồm cả devDependencies để build)
# npm ci sẽ cài đặt chính xác từ package-lock.json
RUN npm ci

# Copy toàn bộ mã nguồn
# Điều này nên xảy ra SAU npm ci để tận dụng Docker layer caching
COPY . .

# Sinh Prisma Client
# Đảm bảo Prisma CLI có sẵn từ node_modules hoặc cài global nếu cần
# (Trong trường hợp này, Prisma là dependency nên `npx` sẽ tìm thấy nó)
RUN npx prisma generate

# Build TypeScript project
# Script "build" trong package.json của bạn là "tsc"
RUN npm run build

# (TÙY CHỌN) Xóa devDependencies để giảm kích thước image sau khi build
# RUN npm prune --production

EXPOSE 8000

# Chạy ứng dụng đã biên dịch bằng Node.js
# Dựa trên script "start" của bạn: "node dist/index.js"
CMD ["node", "dist/index.js"]