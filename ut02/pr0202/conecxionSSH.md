# PR0202: Conexión remota con SSH
### 1. Preparación de la máquina y configuración de la red
En la máquina virtual añadimos un nuevo adaptador de red "Adaptador solo anfitrión"

![alt text](image.png)

Encendemos de nuevo la máquina y entramos para configurar el adaptador creado comprobar las direcciones ip.

![alt text](image1.png)






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
```