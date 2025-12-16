# PR0602 – Manipulacion de cadenas en PowerShell

---

## Ejercicio 1: Limpieza básica (mayúsculas, minúsculas y espacios)

### 1. Normalizar a mayúsculas
```bash

PS C:\Users\hugo> $sys = "Windows Server"
PS C:\Users\hugo> $sys.ToUpper()
WINDOWS SERVER

```
### 2. Normalizar a minúsculas
```bash

PS C:\Users\hugo> $user = "ADMINISTRATOR"
PS C:\Users\hugo> $user.ToLower()
administrator


```
### 3. Limpieza de espacios extremos 
```bash

PS C:\Users\hugo> $ip = " 192.168.1.10 "
PS C:\Users\hugo> $ip.Trim()
192.168.1.10

```
### 4. Eliminación total de espacios
```bash

PS C:\Users\hugo> $mac = "00 AA 11 BB 22 CC"
PS C:\Users\hugo> $mac.Replace(" ", "")
00AA11BB22CC
```
### 5. Longitud de la cadena
```bash

PS C:\Users\hugo> $pass = "P@ssw0rd123"
PS C:\Users\hugo> $pass.Length
11
```
## Ejercicio 2: Reemplazo y sustitución
### 6. Cambio de separadores de fecha
```bash
PS C:\Users\hugo> $fecha = "2023.10.05"
PS C:\Users\hugo> $fecha.Replace(".", "-")
2023-10-05
```
### 7. Actualización de dominio
```bash
PS C:\Users\hugo> $web = "www.miempresa.es"
PS C:\Users\hugo> $web.Replace(".es", ".com")
www.miempresa.com
```
### 8. Censura de datos
```bash
PS C:\Users\hugo> $tarjeta = "1234-5678-9012-3456"
PS C:\Users\hugo> $tarjeta.Substring(0, 15) + "XXXX"
1234-5678-9012-XXXX
```
### 9. Cambio de barra de rutas (Linux a Windows)
```bash
PS C:\Users\hugo> $rutaLinux = "/home/usuario/docs"
PS C:\Users\hugo> $rutaLinux.Replace("/", "\")
\home\usuario\docs
```
### 10. Doble reemplazo (limpiar prefijo y sufijo)
```bash
PS C:\Users\hugo> $valor = "(Software)"
PS C:\Users\hugo> $valor.Replace("(", "").Replace(")", "")
Software
```
## Ejercicio 3: Extracción por posición
### 11. Extraer prefijo de país
```bash
PS C:\Users\hugo> $tlf = "+34-600111222"
PS C:\Users\hugo> $tlf.Substring(0, 3)
+34
```
### 12. Extraer año fiscal (primeros 4 caracteres)
```bash
PS C:\Users\hugo> $codigo = "2024-FACTURA-SEP"
PS C:\Users\hugo> $codigo.Substring(0, 4)
2024
```
### 13. Ignorar el primer carácter
```bash
PS C:\Users\hugo> $idEmpleado = "E55421"
PS C:\Users\hugo> $idEmpleado.Substring(1)
55421
```
### 14. Extraer extensión de archivo (últimos 3)
```bash
PS C:\Users\hugo> $fichero = "informe.pdf"
PS C:\Users\hugo> $fichero.Substring($fichero.Length - 3)
pdf
```
### 15. Relleno de ceros (Padding)
```bash
PS C:\Users\hugo> $numero = "7"
PS C:\Users\hugo> $numero.PadLeft(3, "0")
007
```
## Ejercicio 4: Troceado (Split) y arrays
### 16. Obtener nombre de usuario desde email
```bash
PS C:\Users\hugo> $email = "pepe.garcia@empresa.com"
PS C:\Users\hugo> $email.Split("@")[0]
pepe.garcia
```
### 17. Obtener dominio desde correo electrónico
```bash
PS C:\Users\hugo> $email = "pepe.garcia@empresa.com"
PS C:\Users\hugo> $email.Split("@")[1]
empresa.com
```
### 18. Obtener nombre de archivo de una ruta larga
```bash
PS C:\Users\hugo> $path = "C:\Users\Admin\Downloads\instaler.msi"
PS C:\Users\hugo> $path.Split("\")[-1]
instaler.msi
```
### 19. Obtener letra de unidad
```bash
PS C:\Users\hugo> $path = "D:\Datos\Backups"
PS C:\Users\hugo> $path.Split("\")[0]
D:
```
### 20. Separar CSV manualmente
```bash
PS C:\Users\hugo> $linea = "Juan;Marketing;Madrid"
PS C:\Users\hugo> $linea.Split(";")[1]
Marketing
```
## Ejercicio 5: Aplicaciones prácticas
### 21. Detección de usuario Admin (booleano)
```bash
PS C:\Users\hugo> $u = "ADM_Lopez"
PS C:\Users\hugo> $u.StartsWith("ADM")
True
```
### 22. Formato de nombre propio
```bash
PS C:\Users\hugo> $nombre = "JAVIER"
PS C:\Users\hugo> $nombre.Substring(0,1).ToUpper() + $nombre.Substring(1).ToLower()
Javier
```

### 23. Limpieza de Nombre Distinguido (AD)
```bash
PS C:\Users\hugo> $dn = "CN=Beatriz,OU=Ventas,DC=dominio,DC=local"
PS C:\Users\hugo> $dn.Split(",")[0].Replace("CN=", "")
Beatriz
```
### 24. Generador de iniciales
```bash
PS C:\Users\hugo> $n = "Fernando"; $a = "Alonso"
PS C:\Users\hugo> $n.Substring(0,1) + "." + $a.Substring(0,1) + "."
F.A.
```
### 25. Inversión de fecha
```bash
PS C:\Users\hugo> $euDate = "31-12-2023"
PS C:\Users\hugo> $parts = $euDate.Split("-")
PS C:\Users\hugo> $parts[2] + $parts[1] + $parts[0]
20231231
```

---
[Volver al índice](../../index.md)
