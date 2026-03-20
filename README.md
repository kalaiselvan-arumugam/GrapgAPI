openssl x509 -in microsoft-azure-rsa-tls-ca04.crt -out microsoft-azure-rsa-tls-ca04.pem -inform DER

openssl x509 -in microsoft-azure-rsa-tls-ca04.crt -out microsoft-azure-rsa-tls-ca04.pem

openssl x509 -in microsoft-azure-rsa-tls-ca04.crt \
             -out src/main/resources/certs/ms-azure-tls-ca.pem \
             -inform DER


openssl s_client -connect login.microsoftonline.com:443 -showcerts \
  </dev/null 2>/dev/null \
  | awk '/BEGIN CERT/{f=1} f{print} /END CERT/{f=0}' \
  | awk 'BEGIN{n=0} /BEGIN CERT/{n++} n==2{print}' \
  > src/main/resources/certs/ms-azure-tls-ca.pem
