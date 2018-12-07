```
# sudo echo 1 > /proc/sys/net/ipv4/ip_forward
# iptables -t nat -A POSTROUTING -o enp3s0 -j MASQUERADE
# sudo sysctl net.ipv4.ip_forward=1
# iptables -A FORWARD -o enp3s0 -j ACCEPT
# iptables -A FORWARD -i enp3s0 -j ACCEPT
```
