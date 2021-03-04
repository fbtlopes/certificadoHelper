# certificadoHelper

# Extrai a chave e o certificado de um P12
openssl pkcs12 -in certificado.p12 -out file.key.pem -nocerts -nodes
openssl pkcs12 -in certificado.p12 -out file.crt.pem -clcerts -nokeys

# P12 to keystore.jks
keytool -importkeystore -srckeystore mycert.p12 -srcstoretype PKCS12 -srcstorepass {SENHA} -keystore keystore.jks -storepass {SENHA}

# JKS TO P12
keytool -importkeystore -srckeystore keystore.jks -srcstoretype JKS -deststoretype PKCS12 -destkeystore keystore.p12

# DECODIFICAR CERTIFICADO
Simples: 		openssl x509 -in certificate.crt -text -noout
Toda a cadeia: 		openssl crl2pkcs7 -nocrl -certfile ca.pem | openssl pkcs7 -print_certs -text -noout

# CURL com certificado
curl -k -X POST -E ./file.crt.pem --key ./file.key.pem "URL" -H  "accept: */*" -H  "Content-Type: application/json" -d "{\"id\":\"12345678\"}"

# Trustsore
http://lcrspo.serpro.gov.br/truststore/

# CA
http://lcrspo.serpro.gov.br/cadeias-serpro/
