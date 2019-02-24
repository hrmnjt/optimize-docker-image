FROM golang:1.7.3

WORKDIR /go/src/

RUN go get -d -v golang.org/x/net/html
# You can get a sample app.go file from here (https://gist.github.com/prmishra/b7010ce6c97adc567f28767756efbf4d).
# Do not hardcode app.go file into your Dockerfile as during evaluation we will use a different app.go file.
COPY app.go	.

RUN CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -o app .

WORKDIR /root/

RUN cp /go/src/app    .

CMD ["./app"]
