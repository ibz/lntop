# lntop

[![MIT licensed](https://img.shields.io/badge/license-MIT-blue.svg)](https://github.com/edouardparis/lntop/blob/master/LICENSE)
[![Go Report Card](https://goreportcard.com/badge/github.com/edouardparis/lntop)](https://goreportcard.com/report/github.com/edouardparis/lntop)
[![Godoc](https://godoc.org/github.com/edouardparis/lntop?status.svg)](https://godoc.org/github.com/edouardparis/lntop)
[![tippin.me](https://badgen.net/badge/%E2%9A%A1%EF%B8%8Ftippin.me/@edouardparis/F0918E)](https://tippin.me/@edouardparis)

`lntop` is an interactive text-mode channels viewer for Unix systems.

 ![lntop-v0.0.0](http://paris.iiens.net/lntop-v0.0.0.png?)
 *lntop-v0.0.0*

## Install

Require the [go programming language](https://golang.org/) (version >= 1.11)
```
git clone https://github.com/edouardparis/lntop.git
cd lntop && export GO111MODULE=on && go install -mod=vendor ./...
```

## Config

First time `lntop` is used a config file `.lntop/config.toml` is created
in the user home directory.
```toml
[logger]
type = "production"
dest = "/root/.lntop/lntop.log"

[network]
name = "lnd"
type = "lnd"
address = "//127.0.0.1:10009"
cert = "/root/.lnd/tls.cert"
macaroon = "/root/.lnd/data/chain/bitcoin/mainnet/admin.macaroon"
macaroon_timeout = 60
max_msg_recv_size = 52428800
conn_timeout = 1000000
pool_capacity = 3
```
Change macaroon path according to your network.

## Docker

If you prefer to run `lntop` from a docker container:

```sh
cd docker

# now you should review ./lntop/home/initial-config.toml
# if you have an existing .lntop directory, you can export it
# export LNTOP_HOME=~/.lntop
# ! change path to files in .lntop/config with user current directory /root !

# point LND_HOME to your actual lnd directory
# we recommend using .envrc with direnv
export LND_HOME=~/.lnd

# build the container
./build.sh

# run lntop from the container
./lntop.sh

# lntop data will be mapped to host folder at ./_volumes/lntop-data
```

To see `lntop` logs, you can tail them in another terminal session via:
```sh
./logs.sh -f
```

To start from scratch:
```sh
./clean.sh
./build.sh --no-cache
```

## Compatibility

| lntop  | lightningnetwork/lnd |
|--------|----------------------|
| v0.0.1 | v0.5.1               |
