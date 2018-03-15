# arise 'em
This is a fork of [arise'em](https://github.com/timofurrer/ariseem). Full credit for `ariseem` goes to [Timo Furrer](https://github.com/timofurrer).
This fork provides additional environment variables within the Dockerfile and is published on docker hub.

`ariseem` is a minimalistic service exposing a REST API to boot machines using wake-on-lan.

It's pure Python and does not require any system dependencies.

## Installation

Just use docker:

```
docker build . -t ariseem && docker run -v $PWD:/app --net=host -it ariseem
```

If you want to expose this service into the internet please make sure you are properly secured
with a proxy in front of this service. TLS and at least some form of authentication.

## Configuration

`ariseem` is configured via YAML file:

```
machines:
    myserver: AA:BB:CC:DD:EE:FF
    mypc: AA:BB:CC:FF:EE:DD

groups:
    vpn:
        - myserver
        - mypc
```

`ariseem` can only *wol* machines configured in the `machines` section.
In addition groups of machines can be specified in the `groups` section.

## Usage

```
GET /api/machines
POST /api/machines/myserver

GET /api/groups
POST /api/groups/vpn
```

## Variables

+ `ARISEEM_CONFIG`: path of the config.yml file. Defaults to ./config.yml
+ `FLASK_PORT`: port used by FLASK. Defaults to 5555.
+ `FLASK_DEBUG`
+ `FLASK_APP`
