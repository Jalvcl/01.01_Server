# 01.01 Ubuntu Server Clean

## Instalación desde cero de un servidor Ubuntu Server 16.04 LTS (Xenial Xerus)

### Configuración del Servidor

Instalación desde live server sin seleccionar ninguna opción de programas
Todos los comandos estan ejecutados desde un usuario del grupo sudo

`export TZ=America/Santiago`

### Habilitación repositorios extras

```bash
sudo add-apt-repository universe -y && sudo add-apt-repository restricted -y && sudo add-apt-repository multiverse -y
```

### Instalación de herramientas útiles (opcional)

#### Instalación iTerm integración shell

```sh
curl -L https://iterm2.com/shell_integration/install_shell_integration_and_utilities.sh | bash
```

#### Instalación Tasksel

Utilidad para instalar servicios completos ejemplo LAMP

`sudo apt-get install tasksel -y`

#### Habilitación GUI para uso con Remote Desktop

```bash
sudo apt-get install lxde -y && sudo apt-get install xrdp -y && /etc/init.d/xrdp start
```

## Instalación Docker

Instruciones en:

```sh
https://raw.githubusercontent.com/Jalvcl/02.02_Odoo_Docker/master/instalar_docker.md
```

## Instalación Prometheus

```sh
sudo apt-get update && sudo apt-get install \
    prometheus \
    prometheus-node-exporter \
    prometheus-pushgateway \
    prometheus-alertmanager -y

sudo systemctl start prometheus
sudo systemctl enable prometheus
sudo systemctl status prometheus --no-pager

#correr el monitor en la siguiente dirección
http://localhost:9090
```

## Instalación Grafana

```sh
#editar /etc/apt/sources.list
sudo nano /etc/apt/sources.list
#agrergar la linea
deb https://packagecloud.io/grafana/stable/debian/ xenial main

#sources.list debiera verse similar a esto

deb http://archive.ubuntu.com/ubuntu xenial main universe restricted multiverse
deb http://archive.ubuntu.com/ubuntu xenial-security main universe restricted multiverse
deb http://archive.ubuntu.com/ubuntu xenial-updates main universe restricted multiverse
deb [arch=amd64] https://download.docker.com/linux/ubuntu xenial stable
deb https://packagecloud.io/grafana/stable/debian/ xenial main

#agrergar llave
curl https://packagecloud.io/gpg.key | sudo apt-key add -

#actualizar
sudo apt-get update
#instalar grafana
sudo apt-get install grafana