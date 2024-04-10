FROM node:19.6-bullseye-slim AS base
WORKDIR /ur/src/app
COPY package*.json ./

FROM base AS dev 
RUN --mount=type=cache,target=/usr/src/app/.npm \
    npm set cache /usr/src/app/.npm && \
    npm install
COPY . .
CMD ["npm", "run", "dev"]


FROM base as production
RUN --mount=type=cache,target=/usr/src/app/.npm \
    npm set cache /usr/src/app/.npm && \
    npm ci --only=production
EXPOSE 8080
CMD [ "node", "index.js" ]