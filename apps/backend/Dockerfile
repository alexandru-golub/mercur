FROM node:20-alpine AS build

WORKDIR /app
RUN apk add --no-cache libc6-compat

COPY package*.json ./
RUN npm install --legacy-peer-deps
RUN npm install zod@^3.22.4 --force
COPY . .
RUN npx medusa build


FROM node:20-alpine
WORKDIR /app

COPY --from=build /app ./
EXPOSE 9000

CMD ["npx", "medusa", "start"]
