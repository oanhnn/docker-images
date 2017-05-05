FROM golang:1.8-alpine

ENV NGROK_DOMAIN=ngrok.com

RUN apk update \
 && apk add --no-cache --virtual .build-deps \
        autoconf \
        git \
        make \
        mercurial \
        openssl \

 && mkdir -p /tmp/ngrok /etc/ngrokd \
 && git clone https://github.com/inconshreveable/ngrok.git /tmp/ngrok \
 && cd /tmp/ngrok \

 && openssl genrsa -out base.key 2048 \
 && openssl req -new -x509 -nodes -key base.key -days 10000 -subj "/CN=$NGROK_DOMAIN" -out base.pem \

 
 && openssl genrsa -out server.key 2048 \
 && openssl req -new -key server.key -subj "/CN=$NGROK_DOMAIN" -out server.csr \
 && openssl x509 -req -in server.csr -CA base.pem -CAkey base.key -CAcreateserial -days 10000 -out server.crt \


 && cp base.pem assets/client/tls/ngrokroot.crt \
 && make release-server release-client \
 && chmod a+x bin/ngrokd bin/ngrok \
 && mv server.* base.* /etc/ngrokd/ \
 && mv bin/ngrokd bin/ngrok /usr/local/bin/ \

 && apk del .build-deps \
 && rm -rf /var/cache/apk/* /tmp/*

EXPOSE 80 443 4443

CMD ngrokd -domain="$NGROK_DOMAIN" \
           -tlsKey=/etc/ngrokd/server.key \
           -tlsCrt=/etc/ngrokd/server.crt \
           -httpAddr=":80" \
           -httpsAddr=":443" \
           -tunnelAddr=":4443" \
           -log="stdout" \
           -log-level="WARNING"
