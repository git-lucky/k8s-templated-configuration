FROM golang:1.15-alpine as build-stage

RUN apk --no-cache add \
    g++ \
    git \
    make \
    bash

ARG VERSION
ENV VERSION=${VERSION}

WORKDIR /src
COPY . .
RUN ./scripts/build/build.sh

# Final image.
FROM busybox:latest
# RUN apk --no-cache add \
#     ca-certificates
COPY --from=build-stage /src/bin/k8s-webhook /usr/local/bin/k8s-webhook
ENTRYPOINT ["/usr/local/bin/k8s-webhook"]
