FROM node:18-alpine

WORKDIR /app

# Cài prisma (nếu cần)
RUN npm install -g prisma

COPY package*.json ./
RUN npm install

COPY . .

RUN prisma generate

EXPOSE 8000

CMD ["npm", "run", "dev"]
