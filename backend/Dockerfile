# Sử dụng base image Node.js 20 trên Alpine Linux
FROM node:20-alpine

# Thiết lập thư mục làm việc bên trong container
WORKDIR /app

# Copy package.json và package-lock.json (hoặc npm-shrinkwrap.json)
# Điều này được thực hiện trước để tận dụng Docker layer caching cho dependencies
COPY package*.json ./

# Cài đặt dependencies một cách "sạch sẽ" từ package-lock.json
# Bao gồm cả devDependencies vì chúng cần thiết cho bước build (ví dụ: typescript, prisma)
RUN npm ci

# Copy toàn bộ mã nguồn của ứng dụng vào thư mục làm việc /app
# Điều này nên xảy ra SAU npm ci để tối ưu Docker layer caching.
# Nếu bạn có file .dockerignore, đảm bảo rằng node_modules được ignore.
COPY . .

# Cấp quyền thực thi cho các CLI cần thiết từ node_modules/.bin
RUN chmod +x /app/node_modules/.bin/prisma
RUN chmod +x /app/node_modules/.bin/tsc
# Nếu có nhiều công cụ khác trong node_modules/.bin cần quyền thực thi,
# bạn có thể xem xét một giải pháp tổng quát hơn như:
# RUN find /app/node_modules/.bin -type f -exec chmod +x {} \;
# Hoặc đơn giản là:
# RUN chmod +x /app/node_modules/.bin/*
# Tuy nhiên, việc cấp quyền cụ thể thường an toàn hơn.

# Sinh Prisma Client
# Lệnh này sử dụng Prisma CLI đã được cài đặt như một dependency
RUN npx prisma generate

# Build TypeScript project thành JavaScript
# Script "build" trong package.json của bạn (thường là "tsc") sẽ được thực thi
# Kết quả build thường nằm trong thư mục "dist"
RUN npm run build

# (TÙY CHỌN) Xóa devDependencies để giảm kích thước image cuối cùng
# Bỏ comment dòng dưới nếu bạn muốn làm điều này.
# RUN npm prune --production

# Expose port mà ứng dụng backend sẽ lắng nghe
EXPOSE 8000

# Lệnh để chạy ứng dụng đã biên dịch khi container khởi động
# Dựa trên script "start" của bạn: "node dist/index.js"
CMD ["node", "dist/index.js"]
