Создание самоподписанного сертификата 

openssl genpkey -algorithm RSA -out root-ca.key -pkeyopt rsa_keygen_bits:2048
openssl req -x509 -new -key root-ca.key -out root-ca.crt -days 365 -subj "/CN=Elastic CA"
openssl genpkey -algorithm RSA -out elasticsearch.key -pkeyopt rsa_keygen_bits:2048
openssl req -new -key elasticsearch.key -out elasticsearch.csr -subj "/CN=elasticsearch"
openssl x509 -req -in elasticsearch.csr -CA root-ca.crt -CAkey root-ca.key -CAcreateserial -out elasticsearch.crt -days 365

Конфига подключения:
host: ${ELASTIC_HOST:localhost}
port: ${ELASTIC_PORT:9200}
user: ${ELASTIC_USERNAME:elastic}
password: ${ELASTIC_PASSWORD:pass}