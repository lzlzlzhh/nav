FROM node:22-alpine

WORKDIR /app

RUN apk add --no-cache python3 make g++ cairo-dev jpeg-dev pango-dev giflib-dev pixman-dev

COPY package.json pnpm-lock.yaml .npmrc /app/

RUN npm install -g pm2 tsx pnpm && pnpm install --allow-scripts=all

COPY . /app/

RUN npm run build

VOLUME ["/app/data", "/app/_upload"]

EXPOSE 7777

CMD ["sh", "-c", "npm run init && pm2-runtime start --interpreter tsx src/environments/main.ts"]

