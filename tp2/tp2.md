# TP2 : Utilisation courante de Docker

## I. Commun à tous : App Web

### 🌞 docker-compose.yml

[docker-compose.yml](./I//docker-compose.yml)

# TP2 dév : packaging et environnement de dév local

## 1. Calculatrice

### 🌞 Le lien vers ton dépôt

[calculatrice](https://github.com/danyGhassan/calculatrice_linux)

## 2. Chat room

### 🌞 Packager l'application de chat room

[chat_room](https://github.com/danyGhassan/chat_room_linux)

## 3. Ur own

### 🌞 Packager une application à vous

[hangman_web](https://github.com/danyGhassan/hangman_web)

# TP2 admins : Web stack

## I. Good practices

### 🌞 Limiter l'accès aux ressources
```
danyg@danygThinkPad:~/projets/linux-B2$ docker run --memory=1g --cpus=1 -it test1 bash
root@ef97172a922e:/#  
```

### 🌞 No root

```
danyg@danygThinkPad:~/poubelle$ cat Dockerfile 
FROM nginx:latest
RUN useradd -ms /bin/bash cacaUser
USER cacaUser
WORKDIR /home/cacaUser
```

### 🌞 Mode read-only

```
docker run -d -p 80:80 --read-only -v $(pwd)/nginx-cache:/var/cache/nginx -v $(pwd)/nginx-pid:/var/run cacau_ser_nginx
44d26d172873efac9417ef29085b8395d5da30dff38649b5b88086a679b5d3e0
```
## II. Reverse proxy buddy

## A. Simple HTTP setup

### 🌞 Adaptez le docker-compose.yml de la partie précédente

[docker compose](I/docker-compose.yml)

```
danyg@danygThinkPad:~$ curl www.supersite.com
[{"id":"bob","name":1},{"id":"martin","name":2},{"id":"pikachu","name":3},{"id":"shibboleth","name":4}]
danyg@danygThinkPad:~$ curl www.supersite.com | grep tropdecode
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   104  100   104    0     0  33429      0 --:--:-- --:--:-- --:--:-- 34666
```

## B. HTTPS auto-signé

### 🌞 HTTPS auto-signé