FROM node:alpine

RUN apk update && apk add libc6-compat
RUN GRPC_HEALTH_PROBE_VERSION=v0.2.0 && \
  wget -qO/bin/grpc_health_probe https://github.com/grpc-ecosystem/grpc-health-probe/releases/download/${GRPC_HEALTH_PROBE_VERSION}/grpc_health_probe-linux-amd64 && \
  chmod +x /bin/grpc_health_probe

RUN npm install -g typescript

ARG service_version
ENV SERVICE_VERSION ${service_version:-v1}

WORKDIR /app
COPY ./src/services/rating/package*.json ./
RUN yarn install
COPY ./src/services/rating .

EXPOSE 5007
ENV NODE_ENV production

CMD ["yarn", "start"]
