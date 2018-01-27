# Generar mi registro local

1. Correr container de registro

```bash
$ docker run -d -p 5000:5000 --name registry registry:2
```
2. Bajar una imagen X

```bash
$ docker pull ubuntu
```
3. Renombrar la imagen con un tag pata subirla a nuestro registro local

```bash
$ docker tag ubuntu localhost:5000/mi-imagen:1.0
```
4. Hacer una prueba de push, subiendo la imagen a nuestro registro local.

```bash
$ docker push localhost:5000/mi-imagen:1.0
```
5. Hacer pull de la imagen

```bash
$ docker pull localhost:5000/mi-imagen:1.0
```
6. Destruir el registro local

```bash
$ docker stop registry && docker rm -v registry
```

# Producción

Esta implementación no es para un registro productivo, en caso de que así se quisiera realizar, el container de registry se debe convertir en un servicio local.

Ejemplo con Systemd:

1. Crear un archivo en systemd para el container
```bash
$ sudo vi /etc/systemd/system/registry-container.service
```
2. El archivo debe quedar (ejemplo) de la manera siguiente:
```bash
[Unit]
Description=Registry container
After=docker.service

[Service]
Restart=always
ExecStart=/usr/bin/docker start -a registry
ExecStop=/usr/bin/docker stop -t 2 registry

[Install]
WantedBy=local.target
```
3.- Habilitar el servicio
```bash
$ sudo systemctl enable registry-container.service
```
4. Iniciar el servicio
```bash
$ sudo systemctl start registry-container.service
```
