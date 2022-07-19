1) route-views>show ip route 95.29.149.134
Routing entry for 95.29.128.0/19
  Known via "bgp 6447", distance 20, metric 0
  Tag 6939, type external
  Last update from 64.71.137.241 17:32:22 ago
  Routing Descriptor Blocks:
  * 64.71.137.241, from 64.71.137.241, 17:32:22 ago
      Route metric is 0, traffic share count is 1
      AS Hops 3
      Route tag 6939
      MPLS label: none

route-views>show bgp 95.29.149.134
BGP routing table entry for 95.29.128.0/19, version 2356087476
Paths: (24 available, best #16, table default)
  Not advertised to any peer
  Refresh Epoch 1
  20912 3257 1273 3216 8402
    212.66.96.126 from 212.66.96.126 (212.66.96.126)
      Origin incomplete, localpref 100, valid, external
      Community: 3257:8070 3257:30352 3257:50001 3257:53900 3257:53902 20912:65004
      path 7FE10B0EA518 RPKI State not found
      rx pathid: 0, tx pathid: 0
  Refresh Epoch 1
  3333 1103 3216 8402
    193.0.0.56 from 193.0.0.56 (193.0.0.56)
      Origin incomplete, localpref 100, valid, external
      Community: 3216:2001 3216:4467 8402:1183 65000:52254 65000:65049
      path 7FE0A99AE8C8 RPKI State not found
      rx pathid: 0, tx pathid: 0

2)

echo "dummy" > /etc/modules-load.d/dummy.conf
echo "options dummy numdummies=2" > /etc/modprobe.d/dummy.conf

cat << "EOF" >> /etc/systemd/network/10-dummy0.netdev
[NetDev]
Name=dummy0
Kind=dummy
EOF

cat << "EOF" >> /etc/systemd/network/20-dummy0.network
[Match]
Name=dummy0

[Network]
Address=10.0.8.1/24
EOF

nano /etc/netplan/02-networkd.yaml
network:
  version: 2
  ethernets:
    eth0:
      optional: true
      addresses:
        - 10.0.2.3/24
      routes:
        - to: 10.0.4.0/24
          via: 10.0.2.2

ip r
default via 10.0.2.2 dev eth0 proto dhcp src 10.0.2.15 metric 100
10.0.2.0/24 dev eth0 proto kernel scope link src 10.0.2.3
10.0.2.2 dev eth0 proto dhcp scope link src 10.0.2.15 metric 100
10.0.4.0/24 via 10.0.2.2 dev eth0 proto static
10.0.8.0/24 dev dummy0 proto kernel scope link src 10.0.8.1

ip r | grep static
10.0.4.0/24 via 10.0.2.2 dev eth0 proto static

3)ss -tlnp
State    Recv-Q   Send-Q     Local Address:Port     Peer Address:Port  Process  
LISTEN   0        4096       127.0.0.53%lo:53            0.0.0.0:*              
LISTEN   0        128              0.0.0.0:22            0.0.0.0:*              

53 -DNS
22 -SSH

4) 
ss -unap
State   Recv-Q   Send-Q      Local Address:Port     Peer Address:Port  Process  
UNCONN  0        0           127.0.0.53%lo:53            0.0.0.0:*              
UNCONN  0        0          10.0.2.15%eth0:68            0.0.0.0:*              

53 -DNS
68 -информация от DHSP-сервера


5)

