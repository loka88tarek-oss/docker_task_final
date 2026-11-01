FROM node:18.16.0-slim

WORKDIR /app

COPY package*.json ./
RUN npm install

COPY . .

ARG VITE_BACKEND_SERVER_PROD=http://localhost:5000
ENV VITE_BACKEND_SERVER_PROD=$VITE_BACKEND_SERVER_PROD

RUN npm run build
RUN npm install -g serve

ENV NODE_ENV=production
EXPOSE 4173

CMD ["serve", "-s", "dist", "-l", "4173"]