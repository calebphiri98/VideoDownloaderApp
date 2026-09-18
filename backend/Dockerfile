FROM node:20-slim

# Install ffmpeg and Python (needed for yt-dlp) as root during the image build
RUN apt-get update && \
    apt-get install -y --no-install-recommends ffmpeg python3 python3-pip && \
    rm -rf /var/lib/apt/lists/*

# Install yt-dlp
RUN pip3 install --break-system-packages -U yt-dlp

WORKDIR /app

COPY package*.json ./
RUN npm install --omit=dev

COPY . .

ENV PORT=5000
EXPOSE 5000

CMD ["npm", "start"]
