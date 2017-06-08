# Docker Kerio-Connect

Kerio Connect is Mail/Groupware like Microsoft Exchange, but running on Linux.
More Informations under www.kerio.com/connect

THIS IS A PRIVAT BUILD AND HAS NO CONNECTION TO KERIO COMPANY

USE AT YOUR OWN RISK

## Instructions

Get latest build from Docker:

```bash
docker pull chvb/docker-kerio-connect:latest
```

Or build it by yourself:

```bash
 git clone https://github.com/chvb/docker-kerio-connect.git
 cd docker-kerio-connect
 sudo docker build -t docker-kerio-connect .
```

### Run in background

```bash
$ sudo docker run --name="kerio" \
-p 4040:4040 \
-p 22:22 -p 25:25 -p 465:465 -p 587:587 -p 110:110 -p 995:995 \
-p 143:143 -p 993:993 -p 119:119 -p 563:563 -p 389:389 -p 636:636 \
-p 80:80 -p 443:443 -p 5222:5222 -p 5223:5223 \
-v /#YOUR_KERIO_CONFIGFOLDER:/opt/kerio
-v /#YOUR_KERIO_DATAFOLDER:/kerio_store
-v /#YOUR_KERIO_BACKUP:/backup -t chvb/docker-kerio-connect 
```

### Configure

https://IP-FROM-DOCKER:4040

Stop Kerio Service
```
sudo service kerio-connect stop
```



### Restore Backup

Log in SSH IP Port:4040

Stop Kerio Service
```
sudo service kerio-connect stop
```

Start Recover
```
sudo /opt/kerio/mailserver/kmsrecover /backup
```

Start Kerio Service
```
sudo service kerio-connect start
```

### How to update?

You can remove kerio files/folders in your volume but keep this follow files/folder:


```
*.cfg
mailserver/store
mailserver/dbSSL
mailserver/license
mailserver/settings
mailserver/sslca
mailserver/sslcert
mailserver/ldapmap

```

 
When you pull new images and run. New container will copy new version files/folders of Kerio Connect to your volume but skip files/folders have your settings exists
