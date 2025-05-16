# Use an official Node runtime as a parent image
FROM node:14-slim AS build
# Set the working directory in the container
WORKDIR /usr/src/app

# Copy the package.json and package-lock.json files to the container
COPY package*.json ./

# Install application dependencies
RUN npm install

# Copy the rest of the application code to the container
COPY . .


# Adde muliti-stage build
FROM node:14-slim

WORKDIR /app
COPY --from=build /usr/src/app /app
#expose the port the app runs on

EXPOSE 3000

CMD ["npm", "start"]

