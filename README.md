# Debian Homelab with Docker and Portainer

This repository documents a practical setup for running a self-hosted homelab
on a Debian server using Docker and Portainer.

It is intended as a technical reference and collection of example
Docker Compose (YAML) files for common self-hosted applications.

## Scope

- Debian server preparation
- Docker & Docker Compose installation
- Portainer installation and usage
- Example stacks for self-hosted services

This is **not** a one-click solution. Basic Linux knowledge is required.

---

## Target audience

- Administrators
- Technically experienced users
- Self-hosting enthusiasts

---

## System requirements

- Fresh Debian installation (recommended: Debian stable)
- Root access
- Internet connection

---

## Initial system preparation

Update the system:


```html
apt-get update && apt-get upgrade
```
```html
apt install sudo wget curl htop sudo git mc
```
```html
adduser docker
```
User privilege specification add like here the user docker<br>
```html
visudo
```
root    ALL=(ALL:ALL) ALL<br>
docker  ALL=(ALL:ALL) ALL<br>
```html
usermod -aG sudo docker
```
```html
su docker
```
Install now Docker with the install script from https://github.com/docker/docker-install. In this way you get also the latest version of compose. <br>
```html
sudo curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
```
```html
cd /home/docker
```
Visit here also to see the next steps. https://docs.portainer.io/start/install-ce/server/docker/linux <br>
```html
docker volume create portainer_data
```
Create a network 'proxy' to make all available in the net.<br>
```html
sudo docker network create proxy
```
```html
docker run -d -p 8000:8000 -p 9443:9443 --name portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce:latest
```
```html
id
```
show your ID: uid=1000(docker) gid=1000(docker) groups=1000(docker),27(sudo),100(users)<br>
When you open your https://example.com:9443 you get the info to restart Portainer.
```html
docker stop portainer
```
```html
docker start portainer
```

<P>At this point, the reverse proxy is deployed as a stack via Portainer to route incoming requests to upcoming services.
The first data.yml file is used to create the initial stack.</P>
