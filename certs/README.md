# Certificate Management using Subject Alternative Name

## Make a file - ssl.cnf with following details 

```
[ req ]
default_bits           = 2048
distinguished_name     = req_distinguished_name
req_extensions     = req_ext
prompt = no
[ req_distinguished_name ]
countryName            = IN
stateOrProvinceName    = KA
localityName           = Bangalore
organizationName       = reed
OU = MyDivision
commonName             = raining-lab-1.reed.com
[ req_ext ]
subjectAltName = @alt_names
[alt_names]
DNS.1   = raining-lab-1.reed.com
DNS.2   = raining-lab-2.reed.com
DNS.2   = *.reed.com
```

## To create CSR and Key within first step

```
openssl req -out self-sign.csr -newkey rsa:2048 -nodes -keyout self-sign.key -config `pwd`/openssl.cnf -reqexts req_ext
```

## To create CERT using CSR

```
openssl x509        -signkey self-sign-rsa.key       -in self-sign.csr        -req -days 365 -out self-sign.crt -extfile `pwd`/openssl.cnf -extensions req_ext
```

## Below are optional, incase you need it. 

* To convert RSA

```
openssl rsa -in self-sign.key -out self-sign-rsa.keyout
```

* To ckeck certificate 

```
openssl x509 -in self-sign.crt -text -noout
```
