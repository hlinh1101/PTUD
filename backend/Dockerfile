FROM node:20-alpine

WORKDIR /app

# Cài prisma, typescript toàn cục
RUN npm install -g prisma typescript

# Copy package.json và cài dependencies
COPY package*.json ./
RUN npm install

# Copy mã nguồn
COPY . .

# Sinh Prisma Client
RUN prisma generate

# Biên dịch TypeScript thành JavaScript
RUN npm run build

EXPOSE 8000

# Chạy tệp JavaScript
CMD ["npm", "start"]