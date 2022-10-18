---
title: Extracting certificate and private key files from a .pfx file
date: 2021-10-20
updated: 2022-10-18
tags: cli, certificate, private key
url: extracting-certificate-and-private-key-files-from-a-pfx-file
---

A simple way of extract the certificate and the private key from pfx file

---

The [`PKCS #12` file](https://en.wikipedia.org/wiki/PKCS_12) with **.pfx** or **.p12** extension is an archive file format for storing many cryptography objects, including a private key with its X.509 certificate.

1. Extract the private key from PFX

```bash
openssl pkcs12 -in certificate.pfx -nocerts -out private-key.pem -nodes
```

2. Extract the certificate from PFX

```bash
openssl pkcs12 -in certificate.pfx -nokeys -out certificate.pem
```

**Resources:**
- [PKCS #12 file on wikipedia](https://en.wikipedia.org/wiki/PKCS_12)
- [Extracting Certificate and Private Key Files - University of Washington](https://wiki.cac.washington.edu/display/infra/Extracting+Certificate+and+Private+Key+Files+from+a+.pfx+File)
- [Extract Certificate and Private Key - tecadmin.net](https://tecadmin.net/extract-private-key-and-certificate-files-from-pfx-file/)
- [Extract Certificate and Private Key - tecadmin.net](https://tecadmin.net/extract-private-key-and-certificate-files-from-pfx-file/)
- [What is an SSL Certificate](https://www.digicert.com/what-is-an-ssl-certificate)
