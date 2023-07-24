apt install openssl ssl-cert
mkdir /cert
cd /cert
openssl -req -x509 -new -nodes -out rootcrt.crt -keyout rootkey.key
openssl req -new -nodes -days 365 -out www.csr -keyout www.key
openssl x509 -req -CA rootcrt.crt -CAkey rootkey.key -set_serial 01 -in www.csr -out www.crt
chmod -R 777 /cert/*

atur web apache
buat non-ssl dan ssl
untuk ssl tambahkan
SSLCertificateFile	/etc/ssl/www.crt
SSLCertificateKeyFile	/etc/ssl/www.key
import file rootcrt.crt pada firefox