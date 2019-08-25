# INTERNAL_TAG_REGEXP is a regexp thah mathes semver tags
ARG INTERNAL_TAG_REGEXP="^v(?:\d+\.){2}\d+(?:-(?:beta|alpha)\.\d+)?$"

# Build backend
FROM golang:1.12.5 as build-backend

ARG BACKEND_TAG="master"
ARG BACKEND_VERSION=${BACKEND_TAG}
# Build env vars
ARG CGO_ENABLED=0
ARG GOOS=linux
ARG GOARCH=amd64
# Minio env vars
ARG MINIO_ACCESS_KEY=access-key
ARG MINIO_SECRET_KEY=secret-key
# Test env vars
ARG TEST_STORAGE_S3_ENDPOINT=127.0.0.1:9000
ARG TEST_STORAGE_S3_ACCESS_KEY_ID=access-key
ARG TEST_STORAGE_S3_SECRET_ACCESS_KEY=secret-key
ARG TEST_STORAGE_S3_SECURE=false
#
ARG INTERNAL_TAG_REGEXP

WORKDIR /build/src

# Prepare S3 storage (minio)
RUN mkdir /minio
COPY ./vendor/minio/minio /minio
RUN chmod +x /minio/minio

# Clone tags-drive/core
RUN git clone --branch $BACKEND_TAG --depth 1 --single-branch https://github.com/tags-drive/core /build/src

# Run minio, run tests
RUN bash -c "nohup /minio/minio server data --quiet &" && \
	go test -v -mod=vendor ./...

# Change the version to the latest commit hash if BACKEND_VERSION isn't a semver tag.
# Build a binary in /build directory (must be in the same RUN to correct version setting)
RUN \
	if ! echo ${BACKEND_VERSION} | grep -q -P ${INTERNAL_TAG_REGEXP} ; \
	then \
	BACKEND_VERSION="$(git log --format="%h" -1)" ; \
	echo "Use the latest commit hash instead of tag – ${BACKEND_VERSION}" ; \
	fi && \
	go build -o ../tags-drive -ldflags="-X main.version=${BACKEND_VERSION}" -mod=vendor main.go


# Build frontend
FROM node:12.2.0 as build-frontend

ARG FRONTEND_TAG="master"
ARG VUE_APP_VERSION=${FRONTEND_TAG}
#
ARG INTERNAL_TAG_REGEXP

WORKDIR /build

# Clone tags-drive/web
RUN git clone --branch $FRONTEND_TAG --depth 1 --single-branch https://github.com/tags-drive/web /build

# Change the version to the latest commit hash if VUE_APP_VERSION isn't a semver tag
# Build into /build/dist (must be in the same RUN to correct version setting)
RUN \
	if ! echo ${VUE_APP_VERSION} | grep -q -P ${INTERNAL_TAG_REGEXP} ; \
	then \
	VUE_APP_VERSION="$(git log --format="%h" -1)" ; \
	echo "Use the latest commit hash instead of tag – ${VUE_APP_VERSION}" ; \
	fi && \
	npm i && \
	npm run build


# Build the final image
FROM alpine:3.9.4

RUN apk update && \
	apk add --no-cache tzdata ca-certificates

WORKDIR /app
RUN mkdir /app/web

COPY --from=build-backend /build/tags-drive .
COPY --from=build-frontend /build/dist ./web

EXPOSE 80

ENTRYPOINT [ "./tags-drive" ]
