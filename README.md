# NOT MAINTAINED

This repo is not maintained anymore, please use https://github.com/hortio/docker-blynk

## Docker image (based on openjdk:9-jre-slim) that runs the Blynk server v0.30.2

[![](https://images.microbadger.com/badges/version/pinya/blynk.svg)](https://microbadger.com/images/pinya/blynk "Get your own version badge on microbadger.com")
[![](https://images.microbadger.com/badges/image/pinya/blynk.svg)](https://microbadger.com/images/pinya/blynk "Get your own image badge on microbadger.com")

## Build image

```
docker build -t blynk .
```
## Run image
Create a volume with configuration:

```
docker volume create blynk-server-data
```

Check data volume actual location (by default it will be `/var/lib/docker/volumes/blynk-server-data/_data`): 
Put configuration to `server.properties` in this folder. Possible options are listed here: [https://github.com/blynkkk/blynk-server](https://github.com/blynkkk/blynk-server)

```
docker run --restart=always \
-p 7443:7443 -p 8443:8443 \
-p 8442:8442 -p 8441:8441 \
--mount source=blynk-server-data,target=/data  \
--name blynk -d pinya/blynk
```

## SSL

You can obtain free ssl certificates using [Let's Encrypt Certbot](https://certbot.eff.org/) 

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
