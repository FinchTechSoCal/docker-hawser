# Hawser

<p align="center">
  <img src="https://raw.githubusercontent.com/Finsys/hawser/main/logo/hawser.png" alt="Hawser Logo" width="200">
</p>

[![GitHub Release](https://img.shields.io/github/v/release/Finsys/hawser?style=flat-square&logo=github)](https://github.com/Finsys/hawser/releases/latest)
[![Build](https://img.shields.io/github/actions/workflow/status/Finsys/hawser/build.yml?branch=main&style=flat-square&logo=github&label=build)](https://github.com/Finsys/hawser/actions/workflows/build.yml)
[![Release](https://img.shields.io/github/actions/workflow/status/Finsys/hawser/release.yml?style=flat-square&logo=github&label=release)](https://github.com/Finsys/hawser/actions/workflows/release.yml)
[![Go Version](https://img.shields.io/github/go-mod/go-version/Finsys/hawser?style=flat-square&logo=go)](https://go.dev/)
[![Docker Image](https://img.shields.io/badge/docker-ghcr.io%2Ffinsys%2Fhawser-blue?style=flat-square&logo=docker)](https://github.com/Finsys/hawser/pkgs/container/hawser)
[![License](https://img.shields.io/github/license/Finsys/hawser?style=flat-square)](LICENSE)

Remote Docker agent for [Dockhand](https://dockhand.pro) - manage Docker hosts anywhere.

## Use

We use "Standard Mode with TLS and Token (recommended for production)"

**Pull**

```bash
rm -fr ~/appdata/docker_files/hawser
git clone https://github.com/FinchTechSoCal/docker-hawser.git ~/appdata/docker_files/hawser
```

**Modify .env**
```bash
nano ~/appdata/docker_files/hawser/.env
```

**Generate Keypair**
```bash
openssl req -x509 -newkey rsa:2048 -keyout ~/appdata/hawser/server.key -out ~/appdata/hawser/server.crt -sha256 -days 365 -subj "/C=US"
```




<details>

<summary>Full cert subject</summary>

```bash
openssl req -x509 -newkey rsa:2048 -keyout server.key -out server.crt -sha256 -days 365 -subj "/C=US/ST=State/L=City/O=Organization/CN=yourdomain.com"
```

</details>



<details>

<summary>Old keygen attempt</summary>

```bash
# enter a name for the keypair (hostname)
KEYPATH=~/appdata/hawser
KEYNAME=mykey
# generate a private key
#openssl ecparam -name prime256v1 -genkey -noout -out $KEYPATH/$KEYNAME.key
openssl genrsa -out $KEYPATH/$KEYNAME.key 2048
# extract the public key
#openssl ec -in $KEYPATH/$KEYNAME.key -pubout -out $KEYPATH/$KEYNAME.crt
openssl rsa -in $KEYPATH/$KEYNAME.key -outform PEM -pubout -out $KEYPATH/$KEYNAME.pem
```
</details>
<details>

<summary>Direct docker command</summary>

**Run Hawser**

```bash
docker run -d \
  --name hawser \
  -v /var/run/docker.sock:/var/run/docker.sock \
  -v /path/to/certs:/certs:ro \
  -p 2376:2376 \
  -e TLS_CERT=/certs/server.crt \
  -e TLS_KEY=/certs/server.key \
  -e TOKEN=your-secret-token \
  ghcr.io/finsys/hawser:latest
```
</details>