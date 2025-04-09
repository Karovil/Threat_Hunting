# 🛡 Threat Hunting - Módulo 6: Casos Prácticos y Simulaciones
#  Simulación del Caso XZ y Ataque SSH (Threat Hunting)

##  Instalación de la versión vulnerable de XZ Utils

Para simular el caso de XZ:

🔗 Puedes encontrar la versión vulnerable de **xz-utils 5.6.0** aquí:  
[https://launchpad.net/debian/+source/xz-utils/5.6.0-0.2](https://launchpad.net/debian/+source/xz-utils/5.6.0-0.2)

###  Compilación e instalación

Una vez descargado, dentro del directorio del proyecto ejecuta los siguientes comandos para compilar e instalar:

```bash
./configure
make
sudo make install ```


##  Verificación de versión de XZ

Comprueba que tienes la versión vulnerable instalada ejecutando:

xz --version









