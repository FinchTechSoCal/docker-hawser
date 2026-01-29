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

**Use**
```bash
rm -fr ~/appdata/stacks/hawser
mkdir -p ~/appdata/hawser/
git clone https://github.com/FinchTechSoCal/docker-hawser.git ~/appdata/stacks/hawser
sed -i 's;/path/to/appdata/;'$HOME'/appdata/;g' ~/appdata/stacks/hawser/.env
sed -i 's;YourOwnSuperSecretToken;'$(openssl rand -base64 32)';g' ~/appdata/stacks/hawser/.env
openssl req -x509 -newkey rsa:2048 -keyout ~/appdata/hawser/server.key -out ~/appdata/hawser/server.crt -sha256 -days 3650 -subj "/C=US/ST=California/CN=hawser.io" -nodes
```

**Run**
```bash
docker compose -f ~/appdata/stacks/hawser/docker-compose.yml up -d
```

---

<details>

<summary>Full use</summary>

**Modify .env**
```bash
nano ~/appdata/stacks/hawser/.env
```

**Generate Keypair**
```bash
openssl req -x509 -newkey rsa:2048 -keyout ~/appdata/hawser/server.key -out ~/appdata/hawser/server.crt -sha256 -days 3650 -subj "/C=US/ST=California/CN=hawser.io" -nodes
```

```bash
openssl req -x509 -newkey rsa:2048 -keyout server.key -out server.crt -sha256 -days 365 -subj "/C=US/ST=State/L=City/O=Organization/CN=yourdomain.com" -nodes
```

https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/configuring-https-ssl.html
https://arminreiter.com/2022/01/create-your-own-certificate-authority-ca-using-openssl/
https://docs.redhat.com/en/documentation/red_hat_enterprise_linux/8/html/securing_networks/creating-and-managing-tls-keys-and-certificates_securing-networks#creating-a-private-ca-using-openssl_creating-and-managing-tls-keys-and-certificates

</details>
