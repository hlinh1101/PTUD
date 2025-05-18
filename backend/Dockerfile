FROM node:18-alpine

WORKDIR /app

# 1. Copy và cài dependencies
COPY package*.json ./
RUN npm install

# 2. Copy source
COPY . .

# 3. Cấp quyền thực thi cho prisma và generate
RUN chmod +x ./node_modules/.bin/prisma && npx prisma generate

# 4. Port & lệnh khởi động
EXPOSE 8000
CMD ["npm", "run", "dev"]
