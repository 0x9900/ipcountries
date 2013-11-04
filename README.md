ipcountries
===========

Create a <country_code>.zone.gz file containing all the IP networks
for that country.


__{Net,Free,Open}BSD using pf:__

Add the following rules in your `/etc/pf.conf` file

```
table <badguys> persist
block drop in quick on $out_if from { <badguys> } to any
```

Then you can block any country by adding the IP blocks into the table
`badguys` using the following command:

```
gzcat <country_code>.zone.gz | xargs pfctl -t badguys -T add
```


__Linux:__

```
gzcat <country_code>.zone.gz | awk '{print "iptables -A INPUT -s " $1 " -j REJECT"}' | sh
```
