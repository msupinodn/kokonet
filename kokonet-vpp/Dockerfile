# run example:
# docker run -d -p 5000:5000 --name kokonet-vpp --privileged -v /run/vpp:/run/vpp <image>
FROM rockylinux:9

WORKDIR /app
COPY . /app
COPY fdio-release.repo /etc/yum.repos.d/
COPY supervisord.conf /etc/supervisord.conf

RUN dnf -y update \
  && dnf -y install iproute numactl epel-release python3-pip \
  && dnf -y install supervisor \
  && pip3 install --no-cache-dir flask gunicorn ipaddress cffi \
  && dnf clean all

ENTRYPOINT ["/usr/bin/supervisord", "-c", "/etc/supervisord.conf"]
