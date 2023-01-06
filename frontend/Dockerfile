FROM node:16.19.0 AS builder

WORKDIR /app

RUN apt update && apt install nano -y

COPY . /app

RUN npm install



FROM node:16.19.0-slim

COPY --from=builder /app /app

WORKDIR /app

EXPOSE 3000

CMD ["npm", "start"]