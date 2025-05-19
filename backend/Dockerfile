# ——— Stage 1: build & generate Prisma + transpile TS ———
FROM node:18-alpine AS builder
WORKDIR /app

# 1) Copy manifest và cài cả deps + devDeps
COPY package*.json tsconfig.json ./
RUN npm ci

# 2) Copy code
COPY . .

# 3) Make binaries executable, generate Prisma client và transpile TS
RUN chmod +x node_modules/.bin/prisma node_modules/.bin/tsc \
    && npx prisma generate \
    && npx tsc

# ——— Stage 2: production image ———
FROM node:18-alpine
WORKDIR /app

# 4) Cài production-only deps
COPY package*.json ./
RUN npm ci --omit=dev

# 5) Copy mã js đã build
COPY --from=builder /app/dist ./dist

# 6) Expose và run
EXPOSE 8000
CMD ["node", "dist/index.js"]
