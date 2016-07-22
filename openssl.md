# SYNOPSIS


## Generating CSRs
### Generate a Private Key and a CSR
```sh
openssl req \
       -newkey rsa:2048 -nodes -keyout domain.key \
       -out domain.csr \
       -subj '/CN=domain.com/O=My Company Name LTD./C=US'
```

### Generate a CSR from an Existing Private Key
```sh
openssl req \
       -key domain.key \
       -new -out domain.csr \
       -subj '/CN=domain.com/O=My Company Name LTD./C=US'
```

## Generating SSL Certificates

### Generate Self-Signed Certificate
```sh
openssl req \
  -new -newkey rsa:2048 -days 365 -nodes -x509 \
  -keyout server.key -out server.crt \
  -subj '/CN=domain.com/O=My Company Name LTD./C=US'
```

### Generate a CSR from an Existing Certificate and Private Key
```sh
openssl x509 \
       -in domain.crt \
       -signkey domain.key \
       -x509toreq -out domain.csr
       -subj '/CN=domain.com/O=My Company Name LTD./C=US'
```

### Generate a Self-Signed Certificate from an Existing Private Key
```sh
openssl req \
       -key domain.key \
       -new \
       -x509 -days 365 -out domain.crt
       -subj '/CN=domain.com/O=My Company Name LTD./C=US'
```

### Generate a Self-Signed Certificate from an Existing Private Key and CSR
```sh
openssl x509 \
       -signkey domain.key \
       -in domain.csr \
       -req -days 365 -out domain.crt
       -subj '/CN=domain.com/O=My Company Name LTD./C=US'
```

### View CSR Entries
```sh
openssl req -text -noout -verify -in domain.csr
```

### View Certificate Entries
```sh
openssl x509 -text -noout -in domain.crt
```

### Verify a Certificate was Signed by a CA
```sh
openssl verify -verbose -CAFile ca.crt domain.crt
```




# TERM

### CSR 
Certificate Signing Requests, consists mainly of the public key of a key pair, and some additional information. Both of these components are inserted into the certificate when it is signed




# Ref
1.  [openssl-essentials-working-with-ssl-certificates-private-keys-and-csrs](https://www.digitalocean.com/community/tutorials/openssl-essentials-working-with-ssl-certificates-private-keys-and-csrs)

