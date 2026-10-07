ARG NODE_VERSION=22

# =========================
# Dependencies
# =========================
FROM node:${NODE_VERSION}-alpine AS deps

WORKDIR /app

# Native build tools needed by some npm packages (only in this stage, not in the final image)
# hadolint ignore=DL3018
RUN apk add --no-cache python3 make g++

COPY package*.json ./

# Reproducible, production-only dependency installation
RUN npm ci --omit=dev && npm cache clean --force


# =========================
# Runtime
# =========================
FROM node:${NODE_VERSION}-alpine AS runtime

ENV NODE_ENV=production

# Create the app directory owned by the non-root user
# (WORKDIR alone would create it as root, so the app couldn't write to it)
RUN mkdir -p /app && chown node:node /app
WORKDIR /app

# Run as non-root user
USER node

# Dependencies first, then app code (.dockerignore keeps local node_modules out)
COPY --chown=node:node --from=deps /app/node_modules ./node_modules
COPY --chown=node:node . .

EXPOSE 50051

CMD ["node", "index.js"]
