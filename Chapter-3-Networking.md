# Networking
- `ifconfig`
- `iwconfig`
- `ifconfig eth0 192.168.181.115 netmask 255.255.0.0 broadcast 192.168.1.255`

## Spoofing MAC Address
- `ifconfig eth0 down`
- `ifconfig eht0 hw ether 00:11:22:33:44:55`
- `ifconfig eth0 up`

## IDK what is this
- `dhclient eht0`

## Examining DNS with dig
- `dig hackers-arise.com ns`
- `dig hackers-arise.com mx`

## Changing your DNS Server
- `vim /etc/resolv.conf`
- `vim /etc/hosts`