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

You can ban IPs in iptables:
```
cat /opt/squid-blacklist/ip.txt | awk '{print $2}' | while read i; do iptables -A INPUT --src "$i"/24 -j DROP; done
```

How is blacklist filled up
------------------

Domains:

```
cat /var/log/squid3/access.log | grep HIER_DIRECT | awk '{print $7}' | cut -d/ -f3 | sort | uniq -c | sort -n | tail -n 100
```

IPs

```
cat /var/log/squid3/access.log | grep TCP_DENIED | awk '{print $3}' | cut -d. -f1-3 | sort | uniq -c | sort -n | awk '$1>1000'
```
