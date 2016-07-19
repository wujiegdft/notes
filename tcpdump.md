## 所有的可抓包的设备
```
tcpdump -D
```

## 不显示包的大小, 在eth0上抓取最多100个tcp的包
```
tcpdump -c 100 tcp -s 0 -i eth0 -v -w save.cap
```

## 根据source、destination过滤
```
tcpdump -n dst host 192.168.1.1
tcpdump -n src host 192.168.1.1
tcpdump -n host 192.168.1.1
```

## 根据端口过滤
```
tcpdump -n dst port 23
tcpdump -n dst portrange 1-1023
```

## tcp、udp协议 端口在[1..1023]
```
tcpdump -n tcp dst portrange 1-1023
tcpdump -n udp dst portrange 1-1023
```

## 根据destination的ip和port过滤
```
tcpdump -n "dst host 192.168.1.1 and dst port 23"
tcpdump -n "dst host 192.168.1.1 and (dst port 80 or dst port 443)"
```




http://www.rationallyparanoid.com/articles/tcpdump.html
