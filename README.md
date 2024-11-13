# ssl-localhost
Generate an SSL certificate for localhost, and private IP ranges


## To generate an SSL certificate for localhost and private IP ranges

Create the directories to hold the key/cert files
```
sudo mkdir /etc/ssl/private
sudo mkdir /etc/ssl/certs
```

To create the .cert and .key files for your server, execute the following command, replacing the 192.168.0.79 for the internal IP address of your server if running on a separate machine

```sudo openssl req -x509 -newkey rsa:4096 -sha256 -days 3650 -nodes -keyout /etc/ssl/private/private.key -out /etc/ssl/certs/server.crt -subj "/CN=localhost" -addext "subjectAltName=DNS:localhost,IP:127.0.0.1,IP:::1,IP:192.168.0.79"```

Once the files have been generated, you need to modify your server virtual hosts/server blocks to use them.

## Apache Server
Apache change the following lines to your new certificate locations

```SSLCertificateFile "/etc/ssl/certs/server.crt"
SSLCertificateKeyFile "/etc/ssl/private/private.key"```


## To install certificate on Android devices

Open your device's Settings app.
Tap Security & privacy And then More security settings and then Encryption & credentials.
Tap Install a certificate And then Wi-Fi certificate.
Tap Menu .
Tap where you saved the certificate.
Tap the file.
If needed, enter the key store password. Tap OK.
Enter a name for the certificate.
Tap OK.


# To install certificate on MacOS

Open Keychain Access
Click on File > Import Items
Select the server.crt file created earlier, and enter your password to allow
Then right click on the certificate that was imported, and select get info
Then open the "Trust" section and modify 'When using this certifcate:' to always Trust
