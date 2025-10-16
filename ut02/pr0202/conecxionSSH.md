# PR0202: Conexión remota con SSH
### 1. Preparación de la máquina y configuración de la red
En la máquina virtual añadimos un nuevo adaptador de red "Adaptador solo anfitrión"

<<<<<<< HEAD
![alt text](adaptador.png)

IP de la máquina virtual (Ubuntu):

La interfaz enpos8 es la que corresponde al adaptador de red en modo “red solo anfitrión”.

Su dirección IP es: 192.168.56.106

IP del adaptador en la máquina anfitrión (Windows):

  Adaptador de Ethernet VMware Network Adapter VMnet1:

    Sufijo DNS específico para la conexión. . :

    Vínculo: dirección IPv6 local fe80::8c77:8b3:b4cd:47eb%13

    Dirección IPv4.: 192.168.25.1

    Máscara de subred  : 255.255.255.0
  

![alt text](ipa.png)

Para comprobar la conectividad entre ambos equipos, abre la consola de Windows y ejecuta ping 192.168.56.106. Si recibes respuestas, significa que hay conexión entre el anfitrión y la máquina virtual.

![alt text](conectividad.png)

Para cambiar el nombre del host en Ubuntu, ejecuta el comando sudo hostnamectl set-hostname HGS_server, sustituyendo “HGS” por tus iniciales. Luego edita el archivo /etc/hosts con sudo nano /etc/hosts y añade o modifica la línea 127.0.1.1 HGS_server.

![alt text](hosts.png)

En Windows, para que el nombre del servidor Ubuntu se resuelva localmente, abre el archivo hosts ubicado en C:\Windows\System32\drivers\etc\hosts con permisos de administrador y añade la línea 192.168.56.106 HGS_server. Guarda el archivo y prueba con ping HGS_server desde la consola.

![alt text](hosts2.png)
![alt text](pingHGS.png)

### 2. Creación del usuario y conexión SSH
Para crear el usuario en Ubuntu, abre la terminal y ejecuta el comando sudo adduser HGS_ssh, sustituyendo “HGS” por tus iniciales reales. El sistema te pedirá que introduzcas una contraseña para el nuevo usuario y algunos datos opcionales como nombre completo, número de teléfono, etc. Una vez creado, asegúrate de que el servicio SSH esté instalado y activo. Puedes comprobarlo con sudo systemctl status ssh, y si no está instalado, puedes hacerlo con sudo apt install openssh-server.

Para permitir que el nuevo usuario se conecte mediante SSH con contraseña, simplemente asegúrate de que el archivo /etc/ssh/sshd_config tenga la opción PasswordAuthentication yes habilitada. Si haces cambios en ese archivo, reinicia el servicio SSH con sudo systemctl restart ssh. Luego, desde el equipo anfitrión (Windows), puedes usar una herramienta como PuTTY o el comando ssh HGS_ssh@192.168.56.106 para conectarte, introduciendo la contraseña cuando se te solicite.
Una vez que hayas verificado que la conexión por contraseña funciona correctamente, puedes configurar la autenticación mediante claves pública y privada. Para ello, desde el equipo anfitrión, ejecuta ssh-keygen y genera un par de claves. Luego copia la clave pública al servidor Ubuntu con el comando ssh-copy-id HGS_ssh@192.168.56.106. Esto permitirá que el usuario se conecte sin necesidad de introducir la contraseña cada vez.
### 3. Conexión transparente a Github


Cuando ya tengas configurada la autenticación por clave en Ubuntu, puedes aplicar el mismo método para conectarte a GitHub sin contraseña. Accede a tu cuenta de GitHub, ve a tu perfil, entra en “Settings” y luego en “SSH and GPG keys”. Allí puedes añadir tu clave pública (el contenido del archivo ~/.ssh/id_rsa.pub). Una vez guardada, podrás clonar, hacer push y pull desde tus repositorios sin tener que introducir tu usuario y contraseña cada vez.
=======
Encendemos de nuevo la máquina y entramos para configurar el adaptador creado comprobar las direcciones ip.








Para cambiar el hostname de la máquina abrimos una terminal y utilizamos el comando hostnamectl:
```bash
usuario@hugo:~$ sudo hostnamectl set-hostname hgs_server
usuario@hugo:~$ sudo hostnamectl
 Static hostname: hgsserver
 Pretty hostname: hgs_server
       Icon name: computer-vm
         Chassis: vm
      Machine ID: a626621cad4e40a694106590139e8181
         Boot ID: bd5dcb048ef94f44b3010c37487d8360
  Virtualization: oracle
Operating System: Ubuntu 22.04.3 LTS
          Kernel: Linux 5.15.0-84-generic
    Architecture: x86-64
 Hardware Vendor: innotek GmbH
  Hardware Model: VirtualBox
>>>>>>> 2678831920c4a938cf38e5391fbff7efe2a7a1cd
```
