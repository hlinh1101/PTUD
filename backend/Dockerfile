# —— Stage 1: build & generate Prisma + transpile TS ——  
FROM node:18-alpine AS builder
WORKDIR /app

# Copy package và tsconfig
COPY package*.json tsconfig.json ./

# Cài cả dependencies + devDependencies
RUN npm ci

# Copy toàn bộ source code
COPY . .

# Đảm bảo prisma CLI có quyền thực thi, rồi generate client
RUN chmod +x node_modules/.bin/prisma \
    && npx prisma generate

# Transpile TypeScript ra JavaScript vào thư mục dist/
RUN npx tsc

# —— Stage 2: production image ——  
FROM node:18-alpine
WORKDIR /app

# Copy manifest để cài chỉ production deps
COPY package*.json ./
RUN npm ci --omit=dev

# Copy mã đã build từ builder
COPY --from=builder /app/dist ./dist

# Expose port ứng dụng
EXPOSE 8000

# Khởi chạy file JS đã build
CMD ["node", "dist/index.js"]
