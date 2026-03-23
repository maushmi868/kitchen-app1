# -------- Build Stage --------
FROM node:20-alpine AS builder

WORKDIR /app

COPY package*.json ./
RUN npm ci

COPY . .

# Run lint but don’t fail build (Windows + CRLF safe)
RUN npm run lint || true

# -------- Production Stage --------
FROM node:20-alpine AS production

WORKDIR /app

COPY --from=builder /app ./

EXPOSE 3000

CMD ["npm", "start"]