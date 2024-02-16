## Converter pb7

openssl pkcs7 -inform der -in yourCert.p7b -print_certs -out yourCert.pem


## Instalar certificados no linux
```sh
Go to /usr/local/share/ca-certificates/
Create a new folder, i.e. "sudo mkdir school"
Copy the .crt file into the school folder
Make sure the permissions are OK (755 for the folder, 644 for the file)
Run "sudo update-ca-certificates"
```
## Gerar novos certificados Csr
openssl req -new -newkey rsa:2048 -nodes -keyout server.key -out server.csr

## Converter .cer em .pem
openssl x509 -in cert.cer -out cert.pem


## Gerando requisição de certificado
```sh
openssl req -nodes -newkey rsa:2048 -keyout example.key -out example.csr -subj "/C=GB/ST=London/L=London/O=Global Security/OU=IT Department/CN=example.com"
```
ou 
```sh
#Create client key
openssl genrsa -out client.key 4096

#Create client CSR
openssl req -new -key client.key -out client.csr

```
