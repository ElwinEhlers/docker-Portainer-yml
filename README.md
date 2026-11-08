# Debian-Docker-Host mit Portainer

Dieses Repository dokumentiert die Einrichtung eines Debian-Servers als Docker-Host, verwaltet mit Portainer.

Es dient als technische Referenz und enthält einsatzbereite Docker-Compose-Dateien (YAML) für gängige
selbst gehostete Anwendungen.

## Umfang

- Vorbereitung des Debian-Servers
- Installation von Docker und Docker Compose
- Installation und Nutzung von Portainer
- Beispiel-Stacks für selbst gehostete Dienste

Dies ist **keine** Ein-Klick-Lösung. Grundkenntnisse in Linux werden vorausgesetzt.

---

## Zielgruppe

- Administratoren
- Technisch versierte Anwender
- Betreiber selbst gehosteter Dienste

---

## Voraussetzungen

- Frische Debian-Installation (empfohlen: aktuelles Debian stable)
- Root-Zugriff
- Internetverbindung

---

## Vorbereitung des Systems

System aktualisieren:


```html
apt-get update && apt-get upgrade
```
```html
apt install sudo wget curl htop sudo git mc
```
```html
adduser docker
```
Den Benutzer `docker` in den sudo-Einstellungen eintragen:
```html
visudo
```
```text
root    ALL=(ALL:ALL) ALL
docker  ALL=(ALL:ALL) ALL
```
```html
usermod -aG sudo docker
```
```html
su docker
```
Docker mit dem offiziellen Installationsskript (https://github.com/docker/docker-install) installieren. So erhält man auch
die aktuelle Version von Docker Compose.
```html
sudo curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
```
```html
cd /home/docker
```
Die weiteren Schritte zu Portainer stehen auch in der offiziellen Anleitung:
https://docs.portainer.io/start/install-ce/server/docker/linux
```html
docker volume create portainer_data
```
Ein Netzwerk `proxy` anlegen, über das alle Dienste erreichbar sind:
```html
sudo docker network create proxy
```
```html
docker run -d -p 8000:8000 -p 9443:9443 --name portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce:latest
```
```html
id
```
Zeigt die eigene ID, z. B.: `uid=1000(docker) gid=1000(docker) groups=1000(docker),27(sudo),100(users)`

Beim ersten Aufruf von https://example.com:9443 fordert Portainer gegebenenfalls einen Neustart:
```html
docker stop portainer
```
```html
docker start portainer
```

Anschließend wird der Reverse Proxy als Stack über Portainer bereitgestellt. Er leitet eingehende Anfragen an die folgenden
Dienste weiter. Die erste YAML-Datei dient dazu, diesen ersten Stack anzulegen.
