# How to run your own Homelab via Portainer on a Debian machine.<br>
# yml files for a Homelab
<br>
When you have installed a new Debian and you will run your web applications via Docker follow the next steps.<br>
The web applications can be setup via Portainer.<br>
For the setup of the web applications I will share my X.yml files with you. <br>Those can be used to create a stack, a comfortable way to apply your Docker applications under Portainer.<p>

```html
apt-get update && apt-get upgrade
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
apt install wget curl htop sudo git mc
```
Install now Docker with the install script from https://github.com/docker/docker-install. In this way you get also the latest version of compose. <br>
```html
curl -fsSL https://get.docker.com -o get-docker.sh
sh get-docker.sh
```
```html
su docker
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


Now it is time for the nginx-reserve-proxy to grab the upcoming services and here you will use the first data.yml<P>
