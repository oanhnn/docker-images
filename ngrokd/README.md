## Intro

The plan is to create a pair of executables (`ngrok` and `ngrokd`) that are connected with a self-signed SSL cert. Since the client and server executables are paired, you won't be able to use any other `ngrok` to connect to this `ngrokd`, and vice versa.

## DNS

Add two DNS records: one for the base domain and one for the wildcard domain. For example, if your base domain is `domain.com`, you'll need a record for that and for `*.domain.com`.

## Different Operating Systems

If the OS on which you'll be compiling ngrok (that's the server section below) is different than the OS on which you'll be running the client, then you will need to set the GOOS and GOARCH env variables. I run Linux everywhere, so I don't know how to do that. Please Google it or [see the discussion here](https://github.com/inconshreveable/ngrok/issues/84). If you know how to do this and want to add GOOS/GOARCH instructions here, please let me know.

## On Server

MAKE SURE YOU SET `NGROK_DOMAIN` BELOW. Set it to the base domain, not the wildcard domain.

```
NGROK_DOMAIN="my.domain.com"
git clone https://github.com/inconshreveable/ngrok.git
cd ngrok

openssl genrsa -out rootCA.key 2048
openssl req -x509 -new -nodes -key rootCA.key -subj "/CN=$NGROK_DOMAIN" -days 5000 -out rootCA.pem
openssl genrsa -out device.key 2048
openssl req -new -key device.key -subj "/CN=$NGROK_DOMAIN" -out device.csr
openssl x509 -req -in device.csr -CA rootCA.pem -CAkey rootCA.key -CAcreateserial -out device.crt -days 5000

cp rootCA.pem assets/client/tls/ngrokroot.crt
# make clean
make release-server release-client
```

Copy `bin/ngrok` to whatever computer you want to connect from. Then start the server:

```
bin/ngrokd -tlsKey=device.key -tlsCrt=device.crt -domain="$NGROK_DOMAIN" -httpAddr=":8000" -httpsAddr=":8001"
```


## On Client

MAKE SURE YOU SET `NGROK_DOMAIN` BELOW. Set it to the base domain, not the wildcard domain.

```
NGROK_DOMAIN="my.domain.com"
echo -e "server_addr: $NGROK_DOMAIN:4443\ntrust_host_root_certs: false" > ngrok-config
./ngrok -config=ngrok-config 80
```

Or for SSH forwarding: `./ngrok -config=ngrok-config --proto=tcp 22`
