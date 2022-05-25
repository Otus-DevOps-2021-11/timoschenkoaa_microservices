FROM golang:1.13
RUN go get -u github.com/percona/mongodb_exporter
WORKDIR /go/src/github.com/percona/mongodb_exporter
COPY . .
RUN make build

FROM quay.io/prometheus/busybox:latest
COPY --from=0 /go/src/github.com/percona/mongodb_exporter/bin/mongodb_exporter /bin/mongodb_exporter
EXPOSE 9216
ENV DB_SERVER post_db
ENV MONGODB_URI mongodb://${DB_SERVER}:27017
ENTRYPOINT [ "/bin/mongodb_exporter" ]