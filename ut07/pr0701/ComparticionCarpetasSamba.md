# PR0701: Compartición de carpetas con Samba
## Necesitaremmos:
Ubuntu Server 20.04 -> Servidor de Samba
Ubuntu 20.04 Desktop -> Cliente
Windows 10 -> Cliente
## Realizacion
Configuramos la red en Ubuntu Desktop:

![8](/img/8.png)
![9](/img/9.png)

Configuramos en ubuntu server como aparece en las siguientes imagenes, los pasos de la instalacion que no aparezcan aqui es porque que hay que dejarlos como estan y pasar al siguiente paso.
![1](/img/1.png)
![2](/img/2.png)
![3](/img/3.png)
![4](/img/4.png)
![5](/img/5.png)
![6](/img/6.png)

para configurar la red: entramos en 50-netplan.yaml y lo dejamos asi:

![7](/img/10.png)

y para que se apliquen los cambios:

```bash
sudo netplan apply
```

### Instalacion y configuracion del samba

Ahora instalamos el samba en el ubuntu server con:
```bash
sudo apt install samba
```
Para crear los grupos :
``` bash
sudo groupadd gerencia
sudo groupadd administracion
sudo groupadd taller
```
Para crear los usuarios:
```bash 
sudo useradd -m -G gerencia ger01
sudo useradd -m -G administracion adm01
sudo useradd -m -G administracion adm02
sudo useradd -m -G taller tall01
sudo useradd -m -G taller tall02
sudo useradd -m -G taller tall03
```
Para asignarles una contraseña de Samba, usaremos el comando smbpasswd. Nos pedirá una contraseña para cada usuario:
```bash
sudo smbpasswd -a ger01
sudo smbpasswd -a adm01
sudo smbpasswd -a adm02
sudo smbpasswd -a tall01
sudo smbpasswd -a tall02
sudo smbpasswd -a tall03
```
### Creación de carpetas compartidas
Crearemos las carpetas compartidas de los usuarios en  /samba:
```bash
sudo mkdir /samba
sudo mkdir /samba/gerencia
sudo mkdir /samba/Administracion
sudo mkdir /samba/taller
sudo mkdir /samba/publica

```
### Permisos y propietarios
Gestionaremos los permisos de cada carpeta que hemos creado, dandoles permiso al grupo:
```bash
sudo chown root:gerencia /samba/gerencia
sudo chmod 2775 /samba/gerencia
sudo chown root:administracion /samba/Administracion
sudo chmod 2775 /samba/Administracion
sudo chown root:taller /samba/taller
sudo chmod 2775 /samba/taller
sudo chown root:root /samba/publica
sudo chmod 777 /samba/publica
```

### Configuración del fichero smb.conf
Editamos el fichero de configuracion de samba:
```bash
sudo nano /etc/samba/smb.conf
```
y añadimos esto al final del fichero:
``` bash
[Publica]
comment = Carpeta Publica
path = /samba/Publica
browsable = yes
guest ok = yes
read only = yes
write list = ger01
create mask = 0644
directory mask = 0755

[Gerencia]
comment = Carpeta Gerencia
path = /samba/Gerencia
browsable = yes
valid users = @gerencia
read only = no

[Administracion]
comment = Carpeta Administracion
path = /samba/Administracion
browsable = yes
valid users = @administracion
read only = no

[Taller]
comment = Carpeta Taller
path = /samba/Taller
browsable = yes
valid users = @taller adm01 adm02
read only = no
write list = @taller
```
y dentro de [global] añadimos esto:
```bash
map to guest = bad user
```
para ver que todo esta configurado correctamente:
```bash
sudo systemctl restart smbd
sudo systemctl status smbd
```
![11](/img/11.png)

### Acceso desde Linux
Primero crearemos los usuarios locales:
```bash
sudo adduser tall01
sudo adduser tall02
sudo adduser tall03
```
Insatlamos lo siguiente:
``` bash
sudo apt install smbclient
sudo apt install cifs-utils
```
Acceso a Taller
Probamos el acceso:
```bash
smbclient //192.168.100.10/Taller -U tall01
```

![19](/img/19.png)


Salimos y montamos la carpeta compartida:
```bash
sudo mkdir -p /mnt/Taller

sudo mount -t cifs //192.168.100.10/Taller /mnt/Taller -o user=tall01,pass=admin,uid=tall01,noperm
```
Probamos lectura y escritura:
```bash
cd /mnt/Taller
touch prueba.txt
```

Para del acceso a Pública crearemos la carpeta y la montamos:
```bash
mkdir /mnt/Publica
sudo mount -t cifs //192.168.100.10/Publica /mnt/Publica -o guest,uid=tall01,noperm
```
 y comprobamos que si se puede  leer pero NO escribir.
```bash
ls /mnt/Publica/
touch /mnt/Publica/cosa.txt
``` 
![20](/img/20.png)

### Acceso desde Windows
Creamos adm01, adm02 y ger01  y les asignamos la contraseña que les pusimos en samba:

![12](/img/12.png)

Luego accedemos a \\192.168.100.10 desde el explorador de archivos  una vez iniciada sesion con adm01 y comprobamos que podemos acceder a las carpetas correspondientes a cada usuario y a la carpeta pública, pero no a las de los otros grupos.

![18](/img/18.png)

![17](/img/17.png)

Si intentamos acceder con un usuario a una carpeta que no tiene permisos, sale lo siguiente:

![16](/img/16.png)

En la publica podemos ver pero si intentamos crear algo dará error de permisos:

![15](/img/15.png)

---
[Volver al índice](../../index.md)