# Jet
An HTTP/HTTPS proxy integrated with SOCKS v4/v4a/v5, routes requests via GeoIP CN.

> The name "Jet" is inspired by Jet Black from Cowboy Bepop.

> Inspierd by http://www.catonmat.net/http-proxy-in-nodejs/

## What does Jet do?
```
                                      ┌──────────────────────┐
                                      │SOCKS v4/v4a/v5 Proxy │
                                ┌────▶│  (ShadowSocks etc.)  │──────┐
                                │     └──────────────────────┘      │
                                │                                   ▼
     ┌──────────────────┐     ┌───┐                            ┌────────┐
     │ User Application │────▶│Jet│───────────────────────────▶│Internet│
     └──────────────────┘     └───┘                            └────────┘
```

## Requirements

* Node.js > 6.0.0

## Installation

	npm install -g m31271n/jet

> I do not share my open source work at NPM, because of [I’ve Just Liberated My Modules](https://medium.com/@azerbike/i-ve-just-liberated-my-modules-9045c06be67c).

## Setting Appropriate SOCKS Proxy
Change SOCKS Proxy setting via 3 environment variables:

* `JET_SOCKS_ADDR`
* `JET_SOCKS_PORT`
* `JET_SOCKS_TYPE`

By default, Jet needs SOCKS v5 proxy that run at `127.0.0.1:1080`, it means:

* `JET_SOCKS_ADDR=127.0.0.1`
* `JET_SOCKS_PORT=1080`
* `JET_SOCKS_TYPE=5`

## Run Jet
```
# jet runs on 127.0.0.1:9527 by default
shell> jet run

# run jet on another port, like 9600
shell> jet run -h 127.0.0.1 -p 9600
```

## Configure All Your Application To Use Jet.
### For GUI
I think you know how to set this. It's simple.

### For CLI
Suppose that Jet is running at `127.0.0.1:9527`.

```
CHANNEL="http://127.0.0.1:9527"
NO_CHANNEL="localhost,127.0.0.1"

PROXY_ENV="http_proxy ftp_proxy https_proxy all_proxy HTTP_PROXY HTTPS_PROXY FTP_PROXY ALL_PROXY"
NO_PROXY_ENV="no_proxy NO_PROXY"
for envar in $PROXY_ENV; do
	export $envar=$CHANNEL
done

for envar in $NO_PROXY_ENV; do
	export $envar=$NO_CHANNEL
done

unset CHANNEL
unset NO_CHANNEL
unset PROXY_ENV
unset NO_PROXY_ENV
```

Add above script to your shell init file, like `~/.bashrc`. Then `source` it.

> If you are using other shell, set above environment variables by yourself.

## Test The Effects
### Test Jet is Working Or Not
```
shell> curl --proxy localhost:9527 https://www.google.com/
```

If you get right content, then jet is working.

### Test Your Shell Environment Is Set Properly Or Not
```
shell> curl https://www.google.com/
```

If you get right content, then jet is working. And your shell environment is set properly, too.

## Last
You are not alone, we are all fighting for freedom.

## Reference
* [HTTPS connections over proxy servers](http://stackoverflow.com/questions/516323/https-connections-over-proxy-servers)

## LICENSE
GPL-3.0
