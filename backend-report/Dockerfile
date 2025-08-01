# Start from the latest golang base image
FROM golang:1.24.3-alpine as builder

# Set the Current Working Directory inside the container
WORKDIR /app

# Copy go mod and sum files
COPY go.mod go.sum ./

# Download all dependencies. Dependencies will be cached if the go.mod and go.sum files are not changed
RUN go mod download

# Copy the source from the current directory to the Working Directory inside the container
COPY . .

# Build the Go app
RUN CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -o main .


######## Start a new stage from scratch #######
FROM alpine:latest  

RUN apk add --no-cache ca-certificates && update-ca-certificates
RUN addgroup -g 1001 -S servergroup && adduser -u 1001 -S serveruser -G servergroup

WORKDIR /app/

# Copy the Pre-built binary file from the previous stage
COPY --from=builder /app/main .

USER serveruser

# Expose port 8080 to the outside world
EXPOSE 8080

HEALTHCHECK \
  --interval=30s \
  --timeout=5s \
  --start-period=10s \
  --retries=3 \
  CMD wget -q --spider http://localhost:8080/api/v1/health || exit 1

# Command to run the executable
CMD ["./main"] 