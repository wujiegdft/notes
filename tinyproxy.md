```sh
apt install tinyproxy
ip=`hostname -i`; sed "/Allow 127.0.0.1/a Allow ${ip}" /etc/tinyproxy.conf
service tinyproxy reload
```
