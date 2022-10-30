



## Configuration

**Note, if an OS has a dedicated firewall, it should be used instead**

`iptables` need to allow nodes on other networks to access host. The `nginx` node
is considered as a node on a different network from host.

```
sudo iptables -A INPUT -p tcp -s 0.0.0.0/0 --dport 8787 -m conntrack --ctstate NEW,ESTABLISHED -j ACCEPT
sudo iptables -A OUTPUT -p tcp -s 0.0.0.0/0 --sport 8787 -m conntrack --ctstate ESTABLISHED -j ACCEPT
```

Not sure, if this step is really needed

```
sudo iptables -A FORWARD -i docker0 -o eth0 -j ACCEPT
sudo iptables -A FORWARD -i eth0 -o docker0 -j ACCEPT
```

## Testing

**Note, `http://localhost:8686` hits the port exposed by `nginx_simple` which redirects it to `python_simple` @ `8787`**

```
cd python_simple
docker-compose up -d
cd ../nginx_simple
docker-compose up -d
curl http://localhost:8686
```


