# for building the app
FROM golang:1.25-bookworm AS builder

WORKDIR /src

# copy the dependencies
COPY go.* .
# copy the source
COPY main.go .

# build the binary, output will be /src/main
RUN CGO_ENABLED=0 go build -o main .

# for running the app
FROM debian:bookworm

WORKDIR /app

# copy the binary from builder stage
COPY --from=builder /src/main .
# the artifacts for the program to run
COPY public public
COPY templates templates

# Documentation
ENV PORT=5000 INSTANCE_NAME="dov-bear" INSTANCE_HASH=""

EXPOSE ${PORT}

ENTRYPOINT ./main