# ——— Stage 1: build & generate Prisma + transpile TS ———
FROM node:18-alpine AS builder
WORKDIR /app

# Chép package.json & tsconfig để cài cả devDependencies
COPY package*.json tsconfig.json ./

# Cài tất cả (bao gồm typescript, prisma, wrangler…)
RUN npm ci

# Chép source code
COPY . .

# Cho phép prisma CLI chạy được, rồi generate client
RUN chmod +x node_modules/.bin/prisma \
    && npx prisma generate

# Transpile TS → JS
RUN npx tsc

# ——— Stage 2: production image ———
FROM node:18-alpine
WORKDIR /app

# Chép lại đúng manifest để cài chỉ production deps
COPY package*.json ./

# Cài production-only vào /app/node_modules
RUN npm ci --omit=dev

# Copy mã JS đã build từ builder
COPY --from=builder /app/dist ./dist

# Expose port (cần match code của bạn)
EXPOSE 8000

# Chạy file JS đã build
CMD ["node", "dist/index.js"]
