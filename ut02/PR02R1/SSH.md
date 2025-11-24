# PR02R1: Conexión remota con SSH entre redes
# Documentación de la Práctica: Conexión Remota SSH



---

### Paso 3: Configuración de IPs Estáticas y Rutas (Netplan)

![1.png](1.png)
**Captura 1:** Aquí estás en la terminal de `SERVER-A` (ASIR2), dentro de la carpeta `/etc/netplan`. Estás listando los archivos (`ls`) y luego usando `gedit` (con y sin `sudo`) para editar el archivo de configuración `50-cloud-init.yaml`. Los warnings de `libgedit` son solo errores visuales del editor y no afectan a la práctica.

![2.png](2.png)
**Captura 2:** Esta es la configuración Netplan para **SERVER-A** (`50-cloud-init.yaml`).
* Has definido correctamente la IP `192.168.56.10` para la red solo-anfitrión (`enp0s3`).
* Has definido la IP `10.20.0.1` para la red interna (`enp0s8`).
* Lo más importante es la **ruta estática** al final, que le dice al sistema cómo llegar a la red `10.30.0.0/16` (la de SERVER-C) a través de `10.20.0.2` (SERVER-B).

![3.png](3.png)
**Captura 3:** Esta es la configuración Netplan para **SERVER-B** (probablemente `01-network-manager-all.yaml`).
* Has configurado las dos interfaces, cada una en una red interna distinta: `enp0s3` con `10.20.0.2` y `enp0s8` con `10.30.0.1`.
* Es correcto que esta máquina (el router) no lleve rutas estáticas, ya que está conectada a ambas redes.

![4.png](4.png)
**Captura 4:** Esta es la configuración Netplan para **SERVER-C** (probablemente también `01-network-manager-all.yaml`).
* Has definido su IP `10.30.0.2` en la interfaz `enp0s3`.
* Has añadido la **ruta estática de vuelta** hacia la red `10.20.0.0/16` (la de SERVER-A) a través de `10.30.0.1` (SERVER-B).

---

### Paso 5: Crear los Usuarios e Instalar SSH

![5.png](5.png)
**Captura 5:** Aquí estás en **SERVER-A** creando tu usuario personal (`Hugo_Garcia`). El comando `adduser` inicialmente no permitía mayúsculas o espacios, pero lo has resuelto correctamente usando la opción `--allow-bad-names`.

![6.png](6.png)
**Captura 6:** Creación del usuario `sysadmin` en una de las otras máquinas (probablemente **SERVER-B**), ejecutado como superusuario (`root`).

![7.png](7.png)
**Captura 7:** Creación del usuario `sysadmin` en la otra máquina (probablemente **SERVER-C**), ejecutado con `sudo` desde tu cuenta de `alumno`.

![8.png](8.png)
**Captura 8:** Verificación de que el servidor SSH está instalado y funcionando en una de las máquinas (probablemente `SERVER-A`, como preparación para el paso 6). El comando `systemctl status ssh` muestra que está `active (running)`, lo cual es perfecto.

---

### Paso 6: Conexión Transparente (Host -> SERVER-A)

![10.png](10.png)
**Captura 10:** Este es el primer paso en tu máquina anfitriona (Windows PowerShell). Estás usando `ssh-keygen` para generar tu par de claves pública y privada. Las claves se han guardado correctamente en la ruta por defecto `C:\Users\hugo\.ssh\`.

![9.png](9.png)
**Captura 9:** Aquí estás ejecutando el comando (la alternativa manual a `ssh-copy-id`) para copiar tu clave pública (`id_rsa.pub`) a `SERVER-A`.
* Te conectas como el usuario `hugo` a la IP `192.168.56.10`.
* El sistema te advierte que es la primera vez que te conectas (`The authenticity of host...`).
* Tras aceptar (`yes`), te pide la contraseña del usuario `hugo` en `SERVER-A` para finalizar la copia de la clave.



## Explicación de Ficheros Relacionados con SSH

| Fichero | Ubicación Típica | Contenido y Propósito |
| :--- | :--- | :--- |
| **`~/.ssh/id_rsa`** | Cliente SSH | **Clave privada** del usuario. Es la "llave" secreta utilizada para la autenticación por clave. Debe tener permisos muy restringidos . |
| **`~/.ssh/id_rsa.pub`** | Cliente SSH | **Clave pública** del usuario. Se comparte y se copia en los servidores remotos para permitir el acceso sin contraseña. |
| **`~/.ssh/authorized_keys`** | Servidor SSH | Lista de **claves públicas** autorizadas a iniciar sesión como el usuario propietario de este archivo. Si la clave privada correspondiente es presentada por un cliente, se permite el acceso. |
| **`~/.ssh/known_hosts`** | Cliente SSH | Almacena las **claves de host**  de los servidores a los que te has conectado. Se utiliza para verificar la identidad del servidor y detectar posibles ataques *Man-in-the-Middle* . |
| **`/etc/ssh/sshd_config`** | Servidor SSH | Archivo de configuración principal del **daemon SSH**. Controla el comportamiento del servidor, definiendo el puerto de escucha, los métodos de autenticación permitidos, el acceso de *root*. |
| **`/var/log/auth.log`** | Servidor Linux | Registro de todos los eventos de **autenticación** del sistema, incluyendo los intentos y éxitos de conexión SSH. Es esencial para la auditoría de seguridad. |
| **`/etc/hosts.allow`** | Servidor Linux |  Define qué hosts o redes **tienen permitido** el acceso a ciertos servicios de red (incluido SSH, si está configurado). |
| **`/etc/hosts.deny`** | Servidor Linux |  Define qué hosts o redes **tienen prohibido** el acceso a ciertos servicios de red. |

[Volver al índice](../../index.md)