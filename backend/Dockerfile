FROM node:20-slim

# Install ffmpeg, Python (for yt-dlp), and curl (to install Deno)
RUN apt-get update && \
    apt-get install -y --no-install-recommends ffmpeg python3 python3-pip curl unzip && \
    rm -rf /var/lib/apt/lists/*

# Install yt-dlp
RUN pip3 install --break-system-packages -U yt-dlp

# Install Deno — yt-dlp now needs a JS runtime to solve some of YouTube's extraction challenges
RUN curl -fsSL https://deno.land/install.sh | sh
ENV DENO_INSTALL="/root/.deno"
ENV PATH="$DENO_INSTALL/bin:$PATH"

WORKDIR /app

COPY package*.json ./
RUN npm install --omit=dev

COPY . .

ENV PORT=5000
EXPOSE 5000

CMD ["npm", "start"]
