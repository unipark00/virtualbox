```
# sudo echo 1 > /proc/sys/net/ipv4/ip_forward
# sudo sysctl net.ipv4.ip_forward=1

# sudo iptables -t nat -A POSTROUTING -o enp0s3 -j MASQUERADE
# sudo iptables -A FORWARD -o enp0s3 -j ACCEPT
# sudo iptables -A FORWARD -i enp0s3 -j ACCEPT
```
DNS
```
146.11.115.200 153.88.112.200 147.117.20.200 8.8.8.8
```
