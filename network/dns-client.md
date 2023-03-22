# Set up DNS Client solaris 11.4

```
svccfg -s dns/client
svc:/network/dns/client> setprop config/nameserver = net_address: (8.8.8.8 8.8.4.4)
svc:/network/dns/client> select network/dns/client:default
svc:/network/dns/client:default> refresh
svc:/network/dns/client:default> quit


root@solvm:~# svccfg -s system/name-service/switch
svc:/system/name-service/switch> setprop config/host = astring: "files dns"
svc:/system/name-service/switch> select system/name-service/switch:default
svc:/system/name-service/switch:default> refresh 
svc:/system/name-service/switch:default> quit
root@solvm:~# svcadm enable network/dns/client
root@solvm:~# svcadm enable system/name-service/switch
```
