# welcome ahoy Cloud Systems Bremerhaven
Thank you for been here.<br>

How to run your own Homelab via Portainer on a Debian machine.<br>
When you have installed a new Debian and you will run your web applications via Docker follow the next steps.<br>
The web applications can be setup via Portainer.<br>
For the setup of the web applications I will share my X.yml files with you. <br>Those can be used to create a stack, a comfortable way to apply your Docker applications under Portainer.<p>

apt-get update && apt-get upgrade<br>
adduser docker<br>
visudov
User privilege specification add like here the user docker<br>
root    ALL=(ALL:ALL) ALL<br>
docker  ALL=(ALL:ALL) ALL<br>

usermod -aG sudo docker<br>
apt install wget curl htop sudo git mc<br>

Install now Docker with the install script from https://github.com/docker/docker-install. In this way you get also the latest version of compose.<br>
curl -fsSL https://get.docker.com -o get-docker.sh<br>
sh get-docker.sh<br>

su docker<br>
cd /home/docker<br>
Visit here also to see the next steps. https://docs.portainer.io/start/install-ce/server/docker/linux<br>
docker volume create portainer_data<br>
#Create a network 'proxy' to make all available in the net.<br>
sudo docker network create proxy <br>
docker run -d -p 8000:8000 -p 9443:9443 --name portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce:latest<br>
id
show your ID: uid=1000(docker) gid=1000(docker) groups=1000(docker),27(sudo),100(users)


Now it is time for the nginx-reserve-proxy to grab the upcoming services and here you will use the first data.yml<P>
