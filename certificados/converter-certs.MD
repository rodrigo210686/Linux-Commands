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
