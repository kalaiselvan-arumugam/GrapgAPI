openssl x509 -in microsoft-azure-rsa-tls-ca04.crt \
             -out src/main/resources/certs/ms-azure-tls-ca.pem \
             -inform DER
