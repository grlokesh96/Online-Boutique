# =========================
# Dependencies
# =========================
FROM node:24-alpine AS deps

WORKDIR /app

# Native dependencies required by some npm packages
RUN apk add --no-cache python3 make g++

COPY package*.json ./

# Reproducible dependency installation
RUN npm ci --omit=dev && npm cache clean --force


# =========================
# Runtime
# =========================
FROM node:24-alpine AS runtime

WORKDIR /app

# Run as non-root user
USER node

ENV NODE_ENV=production

COPY --chown=node:node --from=deps /app/node_modules ./node_modules
COPY --chown=node:node . .

EXPOSE 50051

CMD ["node", "index.js"]
