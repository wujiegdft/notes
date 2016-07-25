```sh
echo wujie * 999 * > /etc/ppp/chap-secrets
docker run -d --privileged -p 1723:1723 -v /etc/ppp/chap-secrets:/etc/ppp/chap-secrets mobtitude/vpn-pptp
```
