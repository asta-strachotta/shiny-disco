# build stage
FROM golang:1.21 AS builder

WORKDIR /app
# Download Go modules

COPY go.mod go.sum ./
RUN go mod download
# Copy the source code
COPY *.go ./
RUN CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build -o backend

#RUN GOOS=linux GOARCH=amd64 go build -o backend
#RUN go build -o /backend

# final stage
FROM golang:1.21-alpine
WORKDIR /app
COPY --from=builder /app/backend .
#ENTRYPOINT ./goapp
EXPOSE 9000
RUN ls
CMD ["./backend"]