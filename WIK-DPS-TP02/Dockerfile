FROM node:18.11.0
COPY . /usr/src/app
WORKDIR /usr/src/app
RUN npm install
RUN npx tsc
CMD ["node", "./build/index.js"]

