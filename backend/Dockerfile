FROM node:18-alpine
WORKDIR /app

# Set environment
ENV NODE_ENV=production

# Install runtime dependencies used by dist/*
COPY package.json ./
RUN npm install --omit=dev && npm cache clean --force

# Copy built app and public assets (precompiled)
COPY dist ./dist
COPY public ./public

# Expose backend port (adjust if different)
EXPOSE 8080

# Start the server
CMD ["node", "dist/server.js"]
