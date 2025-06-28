# Use official Node.js LTS image
FROM node:18-alpine

RUN apk add --no-cache curl

# Create app directory
WORKDIR /usr/src/app

# Install dependencies
COPY package*.json ./
RUN npm install

# Copy application code
COPY . .

# Expose app port
EXPOSE 3000

# Start the app
CMD ["node", "app.js"]
