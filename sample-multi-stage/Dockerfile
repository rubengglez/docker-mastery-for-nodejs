FROM node:10-alpine as prod
ENV NODE_ENV=production
RUN mkdir -p app && chown -R node:node /app
WORKDIR /app
COPY package.json package-lock*.json ./
RUN npm install --only=prod && npm cache clean --force
COPY . .
CMD ["node", "./bin/www"]

FROM prod as dev
ENV NODE_ENV=development
RUN npm install --only=development
CMD ["./node_modules/nodemon/bin/nodemon.js", "./bin/www", "--inspect:0.0.0.0:9229"]

FROM dev as test
ENV NODE_ENV=development
CMD ["npm", "test"]