# Links úteis:
- [Documentação do OrangePi Zero 3](http://www.orangepi.org/html/hardWare/computerAndMicrocontrollers/service-and-support/Orange-Pi-Zero-3.html)
- [Gravador SSD](https://www.balena.io/etcher/)
- [Manual de instalação do Dcoker](https://docs.docker.com/engine/install/ubuntu/#install-using-the-repository)
- [Manual de instalação do Pi Hole](https://docs.pi-hole.net/main/basic-install/)
- [Manual de instalação do Pi Hole via Dcker](https://github.com/pi-hole/docker-pi-hole/#running-pi-hole-docker)

# Comandos de configuração do OrangePi

- Mudar a senha
```
passwd orangepi
```

- Configurar a rede
```
nmtui
```

# Instalação do Docker

**1. Adiciona chave GPG oficial do Docker:**
```
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc
```

**2. Adicionar o repositório do Apt:**
```
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

**3. Atualizar a lista de pacotes:**
```
sudo apt-get update
```

**4. Instalar os pacotes do Docker**
```
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin docker-compose
```

**5. Abilitar o Docker subir na inicialização**
```
sudo systemctl enable docker
```

# Desabilitar o Dns local para liberar o porta 53
```
systemctl status dnsmasq
sudo systemctl disable dnsmasq.service
sudo systemctl stop dnsmasq
```

# Instalação do Pi Hole
- Editar o arquivo docker-compose.yaml e colocar a senha do admin

- Copiar o arquivo do Docker-compose para o OrangePi via scp
```
scp docker-compose.yaml orangepi@192.168.0.2:/home/orangepi/docker-compose.yaml
```

- Conectar no OrangePi via ssh
```
ssh orangepi@192.168.0.2
```

- Subir o Pi Hole com o Docker Compose
```
docker-compose up
``` 

- Configurar o servidor Dhcp do roteador para apontar o dns primário para o Pi Hole.
