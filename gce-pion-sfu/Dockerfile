FROM marketplace.gcr.io/google/debian10:latest

RUN apt-get update
RUN apt-get install -y \
    apt-utils \
    curl \
    git \
    wget \
    && rm -rf /var/lib/apt/lists/*
RUN cd /tmp \
    && wget "https://dl.google.com/go/$(curl 'https://golang.org/VERSION?m=text').linux-amd64.tar.gz" \
    && tar -C /usr/local -xzf /tmp/go1.16.linux-amd64.tar.gz \
    && rm /tmp/go1.16.linux-amd64.tar.gz \
    && cd /tmp \
    && git clone https://github.com/tmiv/ion-sfu.git --branch gce --single-branch sfu \
    && cd sfu \
    && git checkout 4dc9c12 \
    && /usr/local/go/bin/go build -o bin/sfu -ldflags "-s -w" ./cmd/signal/json-rpc/main.go \
    && cp bin/sfu /srv/ \
    && cp config.template.toml /srv/ \
    && cp start-sfu.sh /srv/ \
    && cd /tmp \
    && rm -rf sfu \
    && rm -rf /root/go \
    && rm -rf /usr/local/go
CMD /srv/start-sfu.sh
