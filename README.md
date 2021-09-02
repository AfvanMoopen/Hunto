# Hunto
Nmap to scan hidden networks (Onion)

# Hunto





* container boots
* launches Tor and dnsmasq as daemons.
* script then waits for the Tor SOCKS proxy to be up before executing your command.



By default, args to `docker run` are passed to nmap
which calls nmap with args `-sT -PN -n "$@"` necessary for it to work over Tor 




``` bash
docker run --rm -it hunto/onion-nmap -p 80,443 does-hdfi.onion
```

will be executed as:

``` sh
proxychains4 -f /etc/proxychains.conf /usr/bin/nmap -sT -PN -n -p 80,443 does-hdfi.onion
```


# ENV  VAR 
 - DEBUG-LEVEL
 

### Example:

``` bash
$ docker run --rm -it hunto/onion-nmap -p 80,443 facebookcorewwwi.onion
[tor_wait] Wait for Tor to boot... (might take a while)
[tor_wait] Done. Tor booted.
[nmap onion] nmap -p 80,443 facebookcorewwwi.onion
[proxychains] config file found: /etc/proxychains.conf
[proxychains] preloading /usr/lib/libproxychains4.so
[proxychains] DLL init: proxychains-ng 4.12

Starting Nmap 7.60 ( https://nmap.org ) at 2017-10-23 16:17 UTC
[proxychains] Dynamic chain  ...  127.0.0.1:9050  ...  facebookcorewwwi.onion:443  ...  OK
[proxychains] Dynamic chain  ...  127.0.0.1:9050  ...  facebookcorewwwi.onion:80  ...  OK
Nmap scan report for does-hdfi.onion (224.0.0.1)
Host is up (2.7s latency).

PORT    STATE SERVICE
80/tcp  open  http
443/tcp open  https

Nmap done: 1 IP address (1 host up) scanned in 3.58 seconds
```
