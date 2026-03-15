# run:
# docker run -e VPP_CONTROLLER_URL=<vpp controller ip> -e VPP_VTEP_IP=<vpp ip>
FROM python:3.12-alpine

WORKDIR /app
COPY requirements.txt /app/

RUN apk add --no-cache --update \
	build-base \
  && pip install --no-cache-dir -r /app/requirements.txt \
  && apk del build-base

COPY . /app

RUN addgroup -S kokonet && adduser -S kokonet -G kokonet

EXPOSE 80
CMD ["/usr/local/bin/gunicorn", "--log-file", "-", "--bind", "0.0.0.0:80", "server:app"]
