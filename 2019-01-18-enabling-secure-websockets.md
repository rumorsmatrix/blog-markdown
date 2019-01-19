---
title: "Enabling secure websockets"
tags:
  - programming
  - websockets
  - php
  - server admin
---

I've been playing around with [vakata/websocket](https://github.com/vakata/websocket) and after I got it working nicely, I wanted to switch to WSS (websockets over TLS) for a little extra security. Luckily, I already have all the certificates needed thanks to [LetsEncrypt](https://letsencrypt.org/).

## How to enable WSS connections
Find your SSL certificate PEM files; on my Debian (Stretch) server, the certificates are located in `/etc/letsencrypt/live/yourdomain.name/`.

From this directory, you need to `cat` together `fullchain.pem` and `privkey.pem` and place the resulting file somewhere accessible by your websockets server script (but not publically served). Additionally, make sure you add this file to your `.gitignore` file. 

```
cat /etc/letsencrypt/live/yourdomain.name/fullchain.pem /etc/letsencrypt/live/yourdomain.name/privkey.pem cert.pem
echo 'cert.pem' >> .gitignore
```

With this in place, you can now use `wss://` as the protocol and the path to the newly cat'd certificate file in your `\vakata\websocket\Server` constructor:

```
$server = new \vakata\websocket\Server('wss://yourdomain.name:8080', 'cert.pem');
```

Bear in mind, secure websocket connections can only be made from secure web pages -- but if you have the certificates, you're probably already serving pages over HTTPS, right?