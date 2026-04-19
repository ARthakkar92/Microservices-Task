FROM node:18-alpine
WORKDIR /app
COPY package*.json ./
run npm install --production
COPY . .
EXPOSE 3003
CMD ["node" , "app.js"]
