squid-blacklist
===============

Squild Domains Blacklist based on public proxy server experience

Install
--------------
Clone this repo to some folder:

```
cd /opt
git clone https://github.com/sumatipru/squid-blacklist.git
```

Configure your squid to use this blacklist:

```
acl black_domains dstdomain "/opt/squid-blacklist/blacklist.txt"
http_access deny black_domains
```
