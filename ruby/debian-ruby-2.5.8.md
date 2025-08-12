# Installing Ruby 2.5.8 on Debian 12 / Ubuntu 24.04

The [OpenSSL](https://github.com/openssl/openssl) version included in Debian 12 / Ubuntu 24.04 repositories is 3.0. This causes issues when compiling Ruby 2.5.8,
since older Rubies may require OpenSSL 1.x. when building from source.

## Install Prerequisites

```bash
sudo apt update
sudo apt install build-essential ca-certificates zlib1g-dev libyaml-dev libicu-dev
```

## Install OpenSSL 1.1.1w

Compile and install the latest stable OpenSSL 1.x (OpenSSL 1.1.1w) before installing Ruby 2.5.8.

```bash
wget https://github.com/openssl/openssl/releases/download/OpenSSL_1_1_1w/openssl-1.1.1w.tar.gz
tar xvzf openssl-1.1.1w.tar.gz
cd openssl-1.1.1w
./config --prefix=$HOME/.openssl/1.1.1w --openssldir=$HOME/.openssl/1.1.1w
make
make test
make install
rm -rf $HOME/.openssl/1.1.1w/certs
ln -s /etc/ssl/certs $HOME/.openssl/1.1.1w/certs
```

## Install Ruby 2.5.8

Install Ruby 2.5.8 using [rvm](https://rvm.io/), pointing to the OpenSSL 1.1.1w installed directory.

```bash
rvm install ruby-2.5.8 --with-openssl-dir=$HOME/.openssl/1.1.1w
```

## Motivation

I needed Ruby 2.5.8 to build the [bitcoin.org](https://bitcoin.org/) site locally to test contributions. As of 05/03/2025, this is the required Ruby version to install the dependencies and build the site.
