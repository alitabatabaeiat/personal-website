FROM node:16.15-alpine as builder

RUN npm install -g npm
RUN mkdir -p /app && chown -R node:node /app
WORKDIR /app

USER node

COPY --chown=node:node package.json .
RUN npm install --legacy-peer-deps
COPY --chown=node:node . .
RUN ["npm", "run", "build"]

FROM nginx:alpine
EXPOSE 80
WORKDIR /usr/share/nginx/html
RUN rm -rf ./*
COPY --from=builder /app/public .
ENTRYPOINT ["nginx", "-g", "daemon off;"]