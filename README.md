# Threat Hunting Modulo 6 Casos practicos y simulaciones.

## Para simular el caso de xz.

### Aca pueden encontrar la version vulnerable de xz utils.

https://launchpad.net/debian/+source/xz-utils/5.6.0-0.2

Cuando lo tengan descargado dentro de el directorio que lo contiene ejecutan:

´´´ bash 
./configure
make
sudo make install
´´´ 
con esto lo compilan e instalan

xz --version
con  este pueden ver la version (debe ser la 5.6.0)



Este es el script .sh que pueden usar para simular el ataque ssh

#!/bin/bash

# Configuración
USUARIO="atacante"
IP="127.0.0.1"
PASSWORD="contraseña123"
INTENTOS=20

echo "[*] Simulando $INTENTOS intentos SSH contra $IP con el usuario $USUARIO..."
echo

for i in $(seq 1 $INTENTOS); do
  echo "[$i] Intento SSH #$i"
  sshpass -p "$PASSWORD" ssh -o StrictHostKeyChecking=no -o ConnectTimeout=2 $USUARIO@$IP "echo 'Acceso SSH simulado: $i'"
  sleep 1
done

echo
echo "[+] Simulación terminada."

Para poder ejecutarlo deben tener instalado sshpass

Tambien deben darle permisos para poder ejecutarlo
chmod +x simulador_ssh.sh

para ejecutar el script simplemente:
./simulador_ssh.sh





