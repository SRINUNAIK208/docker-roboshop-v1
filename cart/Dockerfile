FROM node:22-alpine3.23 as builder 
WORKDIR /app 
COPY package.js .
RUN npm install 
COPY *.js . 

FROM node:22-alpine3.23
WORKDIR /app
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop
COPY --from=builder /app .
USER roboshop
CMD ["node", "server.js"]