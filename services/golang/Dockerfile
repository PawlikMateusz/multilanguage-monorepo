FROM golang:latest as builder

WORKDIR /build

COPY go.mod go.sum ./
RUN go mod download

COPY . .

ARG project
RUN GOOS=linux CGO_ENABLED=0 GOARCH=amd64 go build -a -v -o app $project

# Start a new stage from busybox
FROM busybox:latest

WORKDIR /dist

COPY --from=builder /build/app .

CMD ["./app"]