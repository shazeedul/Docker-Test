# Use the official Node.js image
FROM node:20-alpine

# Set the working directory in the container
WORKDIR /app/react

# Copy the rest of the application code
COPY . .

# Copy package.json and package-lock.json
COPY package.json package-lock.json ./

# Install dependencies
RUN npm install


# Expose port 3000 for the React app
EXPOSE 3000

# Build the application
RUN npm run build

# Start the React app after build
CMD ["npm", "start"]