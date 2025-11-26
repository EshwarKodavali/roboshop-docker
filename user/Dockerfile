FROM node:20.19.5-alpine3.21 AS build
WORKDIR /opt/server
COPY  package.json .
COPY *.js .
RUN npm install


FROM node:20.19.5-alpine3.21
# Create a group and user
WORKDIR /opt/server
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop && \
    chown -R roboshop:roboshop /opt/server
EXPOSE 8080
LABEL com.project="roboshop" \
      component="user" \
      created_by="sai eshwar"
ENV MONGO="true" \
    REDIS_URL='redis://redis:6379' \
    MONGO_URL="mongodb://mongodb:27017/users"
COPY --from=build /opt/server /opt/server
USER roboshop
CMD [ "server.js" ]
ENTRYPOINT [ "node" ]


# FROM node:20
# EXPOSE 8080
# WORKDIR /opt/server
# COPY  package.json .
# COPY *.js .
# RUN npm install
# ENV MONGO="true" \
#     REDIS_URL='redis://redis:6379' \
#     MONGO_URL="mongodb://mongodb:27017/users"
# CMD [ "node", "server.js" ]
