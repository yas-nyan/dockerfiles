
FROM alpine:3.11.6
LABEL maintainer "yas-nyan <yas-nyan@sfc.wide.ad.jp>"
LABEL version="2.16.0"

ENV GOBGPD_VERSION 2.16.0

WORKDIR /gobgpd

# resolve dependency 
RUN apk --update add mtr wget

# get gobgpd
RUN wget "https://github.com/osrg/gobgp/releases/download/v${GOBGPD_VERSION}/gobgp_${GOBGPD_VERSION}_linux_amd64.tar.gz" -O gobgpdbin.tar.gz && \ 
    tar -xvf gobgpdbin.tar.gz && \
    rm gobgpdbin.tar.gz

# move binaries to bin dir
RUN mkdir bin && \ 
    mv /gobgpd/gobgp /gobgpd/bin/ && \
    mv /gobgpd/gobgpd /gobgpd/bin/

# symlink
RUN ln -s /gobgpd/bin/gobgp /usr/local/bin/ && \ 
    ln -s /gobgpd/bin/gobgpd /usr/local/bin/



# add entrypoint
COPY ./entrypoint.sh /gobgpd/
RUN chmod +x /gobgpd/entrypoint.sh

# copy configuration file
COPY ./gobgpd.conf /gobgpd/gobgpd.conf

EXPOSE 179
ENTRYPOINT ["/gobgpd/entrypoint.sh"]