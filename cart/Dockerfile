# FROM node:20
# #this creats and move to that directory
# WORKDIR /app
# COPY package.json .
# COPY *.js .
# RUN npm install
# ENV REDIS_HOST=redis \
#     CATALOGUE_HOST=catalogue \
#     CATALOGUE_PORT=8080
# CMD ["node","server.js"]


FROM node:current-alpine3.23 AS builder
#this creats and move to that directory
WORKDIR /app
COPY package.json .
COPY *.js .
RUN npm install


FROM node:current-alpine3.23
WORKDIR /app
EXPOSE 8080
COPY --from=builder /app /app

# this env is going to be handles in configMapin k8
# ENV MONGO=true \
#     MONGO_URL="mongodb://mongodb:27017/catalogue"
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop
RUN chown -R roboshop:roboshop /app
USER roboshop
ENTRYPOINT ["node"]
CMD ["server.js"]