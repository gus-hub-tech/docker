FROM node:22-alpine
WORKDIR /app

# Copy dependency files first for better cache usage
COPY package.json yarn.lock ./
RUN yarn install --production

# Copy the rest of your application code
COPY . .

# Expose the app port (adjust if your app uses a different port)
EXPOSE 3000

# Run the app
CMD ["node", "./src/index.js"]