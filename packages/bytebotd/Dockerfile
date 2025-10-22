FROM node:20-alpine

WORKDIR /app

# Copy shared package
COPY packages/shared ./shared

# Copy bytebotd package
COPY packages/bytebotd ./bytebotd

# Install dependencies and build shared
WORKDIR /app/shared
RUN npm ci && npm run build

# Install dependencies and build bytebotd
WORKDIR /app/bytebotd
RUN npm ci && npm run build

# Expose port
EXPOSE 3000

# Start the application
CMD ["node", "dist/main.js"]
