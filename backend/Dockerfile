FROM node:18-alpine AS builder

WORKDIR /var/c3d/backend

# Install dependencies and build
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build

# Development stage
FROM node:18-alpine AS development

WORKDIR /var/c3d/backend

# Install dependencies
COPY package*.json ./
RUN npm install

# Copy source code
COPY . .

EXPOSE 3000

CMD ["npm", "run", "dev"]

# Production stage
FROM node:18-alpine AS final

WORKDIR /var/c3d/backend

# Copy package files and install production dependencies
COPY package*.json ./
RUN npm install --omit=dev

# Copy built files from builder
COPY --from=builder /var/c3d/backend/dist ./dist

EXPOSE 3000

CMD ["npm", "start"] 