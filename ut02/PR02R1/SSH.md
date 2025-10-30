# PR02R1: Conexión remota con SSH entre redes

## Explicación de Ficheros Relacionados con SSH

| Fichero | Ubicación Típica | Contenido y Propósito |
| :--- | :--- | :--- |
| **`~/.ssh/id_rsa`** | Cliente SSH | **Clave privada** del usuario. Es la "llave" secreta utilizada para la autenticación por clave. Debe tener permisos muy restringidos (generalmente `600`). |
| **`~/.ssh/id_rsa.pub`** | Cliente SSH | **Clave pública** del usuario. Se comparte y se copia en los servidores remotos para permitir el acceso sin contraseña. |
| **`~/.ssh/authorized_keys`** | Servidor SSH | Lista de **claves públicas** autorizadas a iniciar sesión como el usuario propietario de este archivo. Si la clave privada correspondiente es presentada por un cliente, se permite el acceso. |
| **`~/.ssh/known_hosts`** | Cliente SSH | Almacena las **claves de host** (o *fingerprints*) de los servidores a los que te has conectado. Se utiliza para verificar la identidad del servidor y detectar posibles ataques *Man-in-the-Middle* (MITM). |
| **`/etc/ssh/sshd_config`** | Servidor SSH | Archivo de configuración principal del **daemon SSH (`sshd`)**. Controla el comportamiento del servidor, definiendo el puerto de escucha, los métodos de autenticación permitidos, el acceso de *root*, etc. |
| **`/var/log/auth.log`** | Servidor Linux | Registro de todos los eventos de **autenticación** del sistema, incluyendo los intentos y éxitos de conexión SSH. Es esencial para la auditoría de seguridad. |
| **`/etc/hosts.allow`** | Servidor Linux | (Usado por TCP Wrappers) Define qué hosts o redes **tienen permitido** el acceso a ciertos servicios de red (incluido SSH, si está configurado). |
| **`/etc/hosts.deny`** | Servidor Linux | (Usado por TCP Wrappers) Define qué hosts o redes **tienen prohibido** el acceso a ciertos servicios de red. |