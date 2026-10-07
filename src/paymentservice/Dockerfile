ARG NODE_VERSION=24

# =========================
# Dependencies
# =========================
FROM node:${NODE_VERSION}-alpine AS deps

WORKDIR /app

# Native build tools required by the pprof addon pulled in by @google-cloud/profiler
# hadolint ignore=DL3018
RUN apk add --no-cache python3 make g++

COPY package*.json ./

# Reproducible dependency installation
RUN npm ci --omit=dev && npm cache clean --force


# =========================
# Runtime
# =========================
FROM node:${NODE_VERSION}-alpine AS runtime

WORKDIR /app

# Run as non-root user
USER node

ENV NODE_ENV=production

# The Google Cloud Profiler aborts the process when no GCP project id is available,
# so keep it off by default. Re-enable on GCP with DISABLE_PROFILER= (empty value).
ENV DISABLE_PROFILER=1

COPY --chown=node:node --from=deps /app/node_modules ./node_modules
COPY --chown=node:node . .

EXPOSE 50051

CMD ["node", "index.js"]
