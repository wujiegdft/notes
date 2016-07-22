# SYNOPSIS

## Generating CSR

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

### Generate a CSR from an Existing Certificate and Private Key
```sh
openssl x509 \
       -in domain.crt \
       -signkey domain.key \
       -x509toreq -out domain.csr
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

## View Certificates

### View CSR Entries
```sh
openssl req -text -noout -verify -in domain.csr
```

### View Certificate Entries
```sh
openssl x509 -text -noout -in domain.crt
```

## Verify a Certificate was Signed by a CA

### Verify a Certificate was Signed by a CA
```sh
openssl verify -verbose -CAfile ca.crt domain.crt
```

## Private Keys
### Create a Private Key
```sh
openssl genrsa -out domain.key 2048
openssl genrsa -des3 -out domain.key 2048
openssl rsa -in domain.key -pubout -out domain.pub
```
### Verify a Private Key
```sh
openssl rsa -check -in domain.key
```
### Verify a Private Key Matches a Certificate and CSR
```sh
openssl rsa -noout -modulus -in domain.key | openssl md5
openssl x509 -noout -modulus -in domain.crt | openssl md5
openssl req -noout -modulus -in domain.csr | openssl md5
```
### Encrypt a Private Key
```sh
openssl rsa -des3 \
       -in unencrypted.key \
       -out encrypted.key
```
### Decrypt a Private Key
```sh
openssl rsa \
       -in encrypted.key \
       -out decrypted.key
```

## Convert Certificate Formats
### Convert PEM to DER
```sh
openssl x509 \
       -in domain.crt \
       -outform der -out domain.der
```
### Convert DER to PEM
```sh
openssl x509 \
       -inform der -in domain.der \
       -out domain.crt
```
### Convert PEM to PKCS7
```sh
openssl crl2pkcs7 -nocrl \
       -certfile domain.crt \
       -certfile ca-chain.crt \
       -out domain.p7b
```
### Convert PKCS7 to PEM
```sh
openssl pkcs7 \
       -in domain.p7b \
       -print_certs -out domain.crt
```
### Convert PEM to PKCS12
```sh
openssl pkcs12 \
       -inkey domain.key \
       -in domain.crt \
       -export -out domain.pfx
```
### Convert PKCS12 to PEM
```sh
openssl pkcs12 \
       -in domain.pfx \
       -nodes -out domain.combined.crt
```

```sh
mkdir CA
cd CA/
mkdir -p ./demoCA/newcerts
touch demoCA/index.txt
touch demoCA/serial
echo 01 > demoCA/serial

openssl req \
  -new -newkey rsa:2048 -days 365 -nodes -x509 \
  -keyout ca.key -out ca.crt \
  -subj '/CN=ca.wujie.com/O=WUJIE LTD./C=US'
  
openssl req \
       -newkey rsa:2048 -nodes -keyout domain.key \
       -out domain.csr \
       -subj '/CN=domain.com/O=My Company Name LTD./C=US'
	
openssl ca -in domain.csr -out domain.crt -cert ca.crt -keyfile ca.key
```

# TERM

### CSR 
Certificate Signing Requests, consists mainly of the public key of a key pair, and some additional information. Both of these components are inserted into the certificate when it is signed


# Ref
1.  [openssl-essentials-working-with-ssl-certificates-private-keys-and-csrs](https://www.digitalocean.com/community/tutorials/openssl-essentials-working-with-ssl-certificates-private-keys-and-csrs)

