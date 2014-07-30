shadowsocks-heroku
==================

shadowsocks-heroku is a lightweight tunnel proxy which can help you get through
 firewalls. It is a port of [shadowsocks](https://github.com/clowwindy/shadowsocks), but
 through a different protocol.

shadowsocks-heroku uses WebSockets instead of raw sockets,
 so it can be deployed on [heroku](https://www.heroku.com/).

Notice that the protocol is INCOMPATIBLE with the origin shadowsocks.

Usage
-----
Deploy script

```
#!/bin/bash
echo "Heroku app name :" 
read YouShadowSocks
heroku login
ssh-keygen -t rsa
heroku keys:add
heroku create $YouShadowSocks
git init
heroku git:remote -a $YouShadowSocks
git add *
git commit -m "*"
git push heroku master

```

Set a few configs:

```
$ heroku config:set METHOD=rc4 KEY=foobar
Setting config vars and restarting still-tor-8707... done, v11
KEY:    foobar
METHOD: rc4
```

Then run:

```
$ node local.js -s still-tor-8707.herokuapp.com -l 1080 -m rc4 -k foobar
shadowsocks-heroku v0.9.6
```

Change proxy settings of your browser into:

    SOCKS5 127.0.0.1:1080

Troubleshooting
----------------

If there is something wrong, you can check the logs by:

    $ heroku logs -t --app still-tor-8707
