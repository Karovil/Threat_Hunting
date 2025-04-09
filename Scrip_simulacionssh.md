
# Simulador de Ataques SSH

Este repositorio contiene el script `.sh` que puedes usar para simular múltiples intentos de acceso SSH fallidos ala maquina para despues  poder monitorearlo.

## 📜 Script

```bash
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
