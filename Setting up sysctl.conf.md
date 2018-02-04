Make the following changes to ```/etc/sysctl.conf```:

Uncomment the following settings:
```

# Prevent some spoofing attacks
net.ipv4.conf.default.rp_filter=1
net.ipv4.conf.all.rp_filter=1

# Do not accept ICMP redirects (prevent MITM attacks)
net.ipv4.conf.all.accept_redirects = 0
net.ipv6.conf.all.accept_redirects = 0

# Do not send ICMP redirects (we are not a router)
net.ipv4.conf.all.send_redirects = 0 

# Log Martian Packets
net.ipv4.conf.all.log_martians = 1

```

Check settings with ```sysctl <settingname>```


```
# Increase the size of the network receive queue
net.core.netdev_max_backlog = 65536
net.core.optmem_max = 65536

# Increase the upper limit on how many connections the kernel will accept.
net.core.somaxconn = 16384

# Increase the memory dedicated to the network interfaces
net.core.rmem_default = 1048576
net.core.wmem_default = 1048576
net.core.rmem_max = 16777216
net.core.wmem_max = 16777216
net.ipv4.tcp_rmem = 4096 87380 16777216
net.ipv4.tcp_wmem = 4096 65536 16777216
net.ipv4.udp_rmem_min = 16384
net.ipv4.udp_wmem_min = 16384

# TCP Fast Open is an extension to the transmission control protocol (TCP) that helps reduce network latency by enabling data to be exchanged during the sender’s initial TCP SYN
net.ipv4.tcp_fastopen = 3

# Increase this to prevent simple DOS attacks
net.ipv4.tcp_max_tw_buckets = 65536

# This setting kills persistent single connection performance and should be turned off
net.ipv4.tcp_slow_start_after_idle = 0

# This helps avoid from running out of available network sockets
net.ipv4.tcp_tw_reuse = 1

# Fast-fail FIN connections which are useless
net.ipv4.tcp_fin_timeout = 15
```





Check https://wiki.archlinux.org/index.php/sysctl for performance settings.