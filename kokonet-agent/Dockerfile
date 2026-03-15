# run:
# docker run -e DATAPLANE_IP=<this node ip> -e ETCD_CLIENT_HOST=<etcd host> -e ETCD_CLIENT_PORT=<port>
FROM python:3.12-alpine

WORKDIR /app
COPY requirements.txt /app/

RUN apk add --no-cache --update \
	build-base \
	wget \
  && pip install --no-cache-dir -r /app/requirements.txt \
  && wget --no-check-certificate https://github.com/redhat-nfvpe/koro/releases/download/v0.2/koro_v0.2_linux_amd64.tar.gz \
  && tar xvfpz koro_v0.2_linux_amd64.tar.gz \
  && cp koro_v0.2_linux_amd64/koro . \
  && rm -rf koro_v0.2_linux_amd64 koro_v0.2_linux_amd64.tar.gz \
  && apk del build-base

COPY . /app

RUN addgroup -S kokonet && adduser -S kokonet -G kokonet

ENTRYPOINT ["/app/agent.py"]
