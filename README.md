# twitter-broadcast (tcast)

## 概念図

```
Twitter REST API -> tcast -> Server 1
                        +--> Server 2
                        +--> Server 3
```

## Setup

### requirements

Install and PATH ...

- sh (bash)
- [jq](https://stedolan.github.io/jq/)
- [twitter/twurl](https://github.com/twitter/twurl)
    - curl-like twitter client
- [cympfh/tw](https://github.com/cympfh/tw)
    - a wrapper of `twurl`

### broadcast destinations

1 line = 1 url (API endpoint)

```
$ cat dest.list
http://localhost:8080/
http://localhost:8081/
http://localhost:8082/api/mastodon/stream
```

### config

```
$ cat config.sh
TCAST_TWITTER_USERNAME=cympfh  # your Twitter username (twurl should be authorized)
TCAST_TIMELINE_INTERVAL=1.4    # interval seconds for timeline requests
TCAST_MENTION_INTERVAL=10
TCAST_DM_INTERVAL=10
```

Every config values have their defaults.

## Usage

```sh
bash ./tcast
```

## Stream

The following data will be streamed

```
{"event_type": "thump"}
{"event_type": "update", "data": {"type": ...}}
{"event_type": "thump"}
{"event_type": "thump"}
:
```

## TODO

- [x] hometimeline
    - [x] text
    - [ ] images
- [ ] mentions
- [ ] DMs
- [ ] notification? (fav, RT)
