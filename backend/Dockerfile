FROM node:18-alpine

WORKDIR /app

# Cài prisma và wrangler CLI (toàn cục)
RUN npm install -g prisma wrangler

# Copy package files & cài đặt dependency
COPY package*.json ./
RUN npm install

# Copy toàn bộ mã nguồn vào container
COPY . .

# Generate Prisma Client
RUN prisma generate

EXPOSE 8000

# Chạy ứng dụng (dev mode)
CMD ["npm", "run", "dev"]
