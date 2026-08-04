

# Programa Nesa Miner. El validador llegará más tarde.
![image](https://github.com/user-attachments/assets/f562e1f3-e6fc-40e1-9166-25b24ea753cf)

# Requisitos del Sistema
- CPU: Procesador multicore
- Memoria: Mínimo 4 GB de RAM
- Almacenamiento: 50 GB de espacio en disco libre (se recomienda más para permitirnos enviar más trabajos con el fin de probar las capacidades de su nodo durante el testnet)
- GPU: Se recomiendan GPUs habilitados para CUDA. También se admite MPS. La minería con CPU está disponible, pero no es válida para todos los modelos.

# Instalemos los requisitos
```console
sudo apt update && sudo apt upgrade -y
sudo apt install jq -y
```
```console
# Docker kuralım
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io
docker version

# Docker-compose kuralım
VER=$(curl -s https://api.github.com/repos/docker/compose/releases/latest | grep tag_name | cut -d '"' -f 4)

curl -L "https://github.com/docker/compose/releases/download/"$VER"/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

chmod +x /usr/local/bin/docker-compose
docker-compose --version
```
# Creamos una cuenta en [HugginFace](https://huggingface.co/) y generamos un Token para guardarlo.
# Hugging Face > Profile > Settings > Access Tokens, al crearlo, otorgamos el permiso de Write.
![image](https://github.com/user-attachments/assets/339bcbba-083b-4a89-b869-2505095197f3)

# Descarguemos y ejecutemos el script de Bootstrap - También abramos el PORT necesario
```console
# Portu açalım
sudo ufw allow 31333

# Script çalıştıralım
bash <(curl -s https://raw.githubusercontent.com/nesaorg/bootstrap/master/bootstrap.sh)
```
# Prosigamos secuencialmente con los siguientes pasos.
- `Wizardy` > `Asigne un nombre` > `ENTER` > `ENTER` > `Miner` > `Ingrese la clave privada del Leap Wallet que comience con 0x` > `NON-Distributed Miner` > `presione ENTER para continuar con el modelo actual o ingrese el nombre del modelo de HugginFace` > `Ingrese la clave TOKEN de Huggingface` > `YES`
- Al ingresar el modelo, debe encontrarlo en HugginFace y aceptar su licencia.

# Verifiquemos el Miner, debe verse así:
```console
docker ps -a
```
![image](https://github.com/user-attachments/assets/4f665208-6bd9-4d9e-8b63-f21526e35953)

# Verifiquemos si el Miner está activo desde el [Explorer](https://node.nesa.ai/) gracias a nuestro `Peer ID`
```console
cat ~/.nesa/identity/node_id.id
```

# ESTO ES TODO POR AHORA, BUENA SUERTE. TAMBIÉN DEJO A CONTINUACIÓN EL GIF DE INSTALACIÓN DEL EQUIPO NESA.
![gif](https://raw.githubusercontent.com/nesaorg/bootstrap/master/images/bootstrap.gif)


# Puede verificar los pasos.
- Ejecute en la Terminal/Línea de Comandos:
- `bash <(curl -s https://raw.githubusercontent.com/nesaorg/bootstrap/master/bootstrap.sh)`
- Wizardy: seleccione esta opción para una instalación rápida
- Moniker: ingrese un nombre para su nodo
- Email: ingrese una dirección de correo electrónico que se asociará con su nodo
- Referral Code: nesa1a87dva92dfzqdxg4gzut006yr7h3ct3z4grnqq
- Refiera a sus amigos proporcionando su dirección de billetera Nesa, que comienza con la palabra Nesa y puede encontrarse en Leap Wallet después de hacer clic en Conectar Billetera en la parte superior de esta página.
- Private Key: ingrese la clave privada del Leap wallet
- HuggingFace API Key: ingrese el Token Id de HuggingFace
- Yes: inicie el nodo con la configuración seleccionada

# SIGA LOS SIGUIENTES PASOS PARA ELIMINAR NESA.
```console
sudo docker stop orchestrator
sudo docker stop ipfs_node
```
```console
sudo docker rm orchestrator
sudo docker rm ipfs_node
```
```console
sudo docker images
```
```console
sudo docker rmi ghcr.io/nesaorg/orchestrator:devnet-latest
sudo docker rmi ipfs/kubo:latest
```
```console
sudo docker image prune -a
```
### Para eliminar todos los contenedores en estado exited en el servidor
```console
sudo docker container prune
```
