# Stage 1: Build React app
FROM node:14-slim AS build

WORKDIR /usr/src/app

COPY package*.json ./
RUN npm install

COPY . .
RUN npm run build

# Stage 2: Serve using 'serve'
FROM node:14-slim

RUN npm install -g serve

WORKDIR /app

# Copy only the build output
COPY --from=build /usr/src/app/build ./build

EXPOSE 3000

CMD ["serve", "-s", "build", "-l", "3000"]
