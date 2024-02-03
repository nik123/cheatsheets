# Linux Networking

Useful Linux commands for networking

Scan devices in given network:
```
sudo nmap -sP 192.168.88.0/24
```

Find program which uses given port:
```
nmap -sV --reason -A -p 5672 localhost
```

List ports in use:
```
sudo netstat -tunlp
# alternative:
sudo ss -tunlp
```

List network interfaces:
```
# Option 1:
ifconfig

# Option 2:
nmcli
```
