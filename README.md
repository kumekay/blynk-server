# Docker image (based on openjdk:8-jre-apline) that runs the Blynk server v0.20.1

[![](https://images.microbadger.com/badges/version/pinya/blynk.svg)](https://microbadger.com/images/pinya/blynk "Get your own version badge on microbadger.com")
[![](https://images.microbadger.com/badges/image/pinya/blynk.svg)](https://microbadger.com/images/pinya/blynk "Get your own image badge on microbadger.com")

## Build image

```
docker build -t blynk .
```
## Run image

```
docker run --restart=always \
-p 7443:7443 -p 8443:8443 \
-p 8442:8442 -p 8441:8441 \
-v /path/to/blynk-server-data:/data \
--name blynk -d pinya/blynk
```

## SSL

You can obtain free ssl certificates using [Let's Encrypt Certbot](https://certbot.eff.org/) or from [StartSSL](https://www.startssl.com/).

Put your `fullchain.crt` and `privkey.pem` to `blynk-data` folder.

Add these lines to `blynk-data/server.properties`
```
server.ssl.cert=/data/fullchain.crt
server.ssl.key=/data/privkey_pass.pem
server.ssl.key.pass=SeCuR3_Pa$$w0rD

https.cert=/data/fullchain.crt
https.key=/data/privkey_pass.pem
https.key.pass=SeCuR3_Pa$$w0rD
```
Don't forget to encrypt your privkey and set password:

```
openssl pkcs8 -topk8 -inform PEM -outform PEM -in privkey.pem -out privkey_pass.pem
```

Good luck!

Original blynk-docker project: https://github.com/mpherg/blynk-server
