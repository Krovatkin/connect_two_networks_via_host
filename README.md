



## Configuration

**Note, if an OS has a dedicated firewall, it should be used instead**

`iptables` need to allow nodes on other networks to access host. The `nginx` node
is considered as a node on a different network from host.

```
sudo iptables -A INPUT -p tcp -s 0.0.0.0/0 --dport 8787 -m conntrack --ctstate NEW,ESTABLISHED -j ACCEPT
sudo iptables -A OUTPUT -p tcp -s 0.0.0.0/0 --sport 8787 -m conntrack --ctstate ESTABLISHED -j ACCEPT
```

