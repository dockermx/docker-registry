# Instalación Nexus

```bash

$ sudo mkdir /app && cd /app

$ sudo wget https://sonatype-download.global.ssl.fastly.net/nexus/3/$nexus-3.8.0-02-unix.tar.gz

$ sudo tar -xvf nexus-3.8.0-02-unix.tar.gz

$ sudo mv nexus-3.8.0-02 nexus

$ sudo adduser nexus

$ sudo chown -R nexus:nexus /app/

$ sudo vi /app/nexus/bin/nexus.rc  -> run as nexus user.

$ sudo ln -s /app/nexus/bin/nexus /etc/init.d/nexus

$ sudo chkconfig --add nexus

$ sudo chkconfig --levels 345 nexus on

$ sudo service nexus start

```