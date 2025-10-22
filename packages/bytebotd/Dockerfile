FROM ubuntu:22.04

# Install system dependencies for Node.js, X11, Xvfb, fonts, and GUI libraries
RUN apt-get update && apt-get install -y \
    curl \
    ca-certificates \
    gnupg \
    # Node.js dependencies
    && mkdir -p /etc/apt/keyrings \
    && curl -fsSL https://deb.nodesource.com/gpgkey/nodesource-repo.gpg.key | gpg --dearmor -o /etc/apt/keyrings/nodesource.gpg \
    && echo "deb [signed-by=/etc/apt/keyrings/nodesource.gpg] https://deb.nodesource.com/node_20.x nodistro main" | tee /etc/apt/sources.list.d/nodesource.list \
    && apt-get update \
    && apt-get install -y nodejs \
    # X11 and Xvfb
    xvfb \
    x11vnc \
    x11-xserver-utils \
    xauth \
    dbus-x11 \
    # Fonts
    fonts-liberation \
    fonts-dejavu-core \
    fonts-noto \
    fonts-noto-cjk \
    fonts-noto-color-emoji \
    fontconfig \
    # GUI and browser dependencies
    libnss3 \
    libnspr4 \
    libatk1.0-0 \
    libatk-bridge2.0-0 \
    libcups2 \
    libdrm2 \
    libdbus-1-3 \
    libexpat1 \
    libxcb1 \
    libxkbcommon0 \
    libx11-6 \
    libxcomposite1 \
    libxdamage1 \
    libxext6 \
    libxfixes3 \
    libxrandr2 \
    libgbm1 \
    libpango-1.0-0 \
    libcairo2 \
    libasound2 \
    libatspi2.0-0 \
    libxshmfence1 \
    # Additional utilities
    xdotool \
    wmctrl \
    procps \
    && rm -rf /var/lib/apt/lists/*

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
