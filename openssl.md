## SYNOPSIS
### Self-signed certificate
```sh
openssl req -new -newkey rsa:2048 -days 365 -nodes -x509 -keyout server.key -out server.crt -subj '/CN=domain.com/O=My Company Name LTD./C=US'
```


## TERM
### CSR 
Certificate Signing Requests, consists mainly of the public key of a key pair, and some additional information. Both of these components are inserted into the certificate when it is signed




### Ref
- [openssl-essentials-working-with-ssl-certificates-private-keys-and-csrs](https://www.digitalocean.com/community/tutorials/openssl-essentials-working-with-ssl-certificates-private-keys-and-csrs)
