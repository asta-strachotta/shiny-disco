FROM golang:1.21 AS builder

WORKDIR /app
COPY go.mod ./
RUN go mod download
COPY . ./
# Copy the source code
COPY *.go ./
RUN CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build -o frontend

#RUN GOOS=linux GOARCH=amd64 go build -o frontend
#RUN go build -o /frontend


FROM golang:1.21-alpine

WORKDIR /app
COPY --from=builder /app/frontend .
COPY --from=builder /app/templates ./templates
COPY --from=builder /app/static ./static

EXPOSE 8080
RUN ls
CMD ["./frontend"]

