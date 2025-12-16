# PR0604: Manipulación de colecciones en powerShell

---

## Bloque I: Matrices fijas

### 1. Reconfiguración de DNS y Verificación
```bash

PS C:\Users\hugo> $dns = @("192.168.1.10","10.0.0.50")
PS C:\Users\hugo> "Configuración actual: $($dns[0]) - $($dns[1])"
Configuración actual: 192.168.1.10 - 10.0.0.50
PS C:\Users\hugo> $dns[1] = "8.8.8.8"
PS C:\Users\hugo> $dns.Count
2
PS C:\Users\hugo> "Configuración final: $($dns[0]) - $($dns[1])"
Configuración final: 192.168.1.10 - 8.8.8.8

```
### 2. Rotación de registros de copias de seguridad (LIFO - Last In, First Out)
```bash
PS C:\Users\hugo> $backups = @("Backup_Lunes.zip","Backup_Martes.zip","Backup_Miercoles.zip")
PS C:\Users\hugo> $oldest = $backups[0]
PS C:\Users\hugo> $newest = $backups[-1]
PS C:\Users\hugo> $backups[-1] = $backups[-1] + " (CORRUPTO)"
PS C:\Users\hugo> "Rotación de copias de seguridad: Del $oldest al $newest"
Rotación de copias de seguridad: Del Backup_Lunes.zip al Backup_Miercoles.zip

```
## Bloque II: Listas de arreglos
### 3. Gestión de Cola de incidencias (Priorización)
```bash
PS C:\Users\hugo> $cola = [System.Collections.ArrayList]::new()
PS C:\Users\hugo> $null = $cola.Add("Monitor parpadea")
PS C:\Users\hugo> $null = $cola.Add("Ratón no va")
PS C:\Users\hugo> $cola.Insert(0,"SERVIDOR CAÍDO")
PS C:\Users\hugo> $null = $cola.Remove("Ratón no va")
PS C:\Users\hugo> $cola
SERVIDOR CAÍDO
Monitor parpadea
PS C:\Users\hugo> $cola.Count
2
```

### 4. Validación de lista negra de IPs (Seguridad)
```bash
PS C:\Users\hugo> $blacklist = [System.Collections.ArrayList]::new()
PS C:\Users\hugo> $null = $blacklist.Add("10.10.10.5")
PS C:\Users\hugo> $null = $blacklist.Add("192.168.50.4")
PS C:\Users\hugo> $null = $blacklist.Add("80.80.80.80")
PS C:\Users\hugo> $nuevaAmenaza = "192.168.50.4"
PS C:\Users\hugo> if ($blacklist -contains $nuevaAmenaza) { "La IP $nuevaAmenaza ya estaba bloqueada. No se hace nada" } else { $null = $blacklist.Add($nuevaAmenaza); "IP $nuevaAmenaza añadida a la lista negra." }
La IP 192.168.50.4 ya estaba bloqueada. No se hace nada
PS C:\Users\hugo> $blacklist | Sort-Object
10.10.10.5
192.168.50.4
80.80.80.80
```

## Bloque III: Listas genéricas
### 5. Hardening de puertos de Firewall (List[int])
```bash
PS C:\Users\hugo> $ports = [System.Collections.Generic.List[int]]::new()
PS C:\Users\hugo> $ports.Add(80)
PS C:\Users\hugo> $ports.Add(443)
PS C:\Users\hugo> $ports.Add(53)
PS C:\Users\hugo> $ports.Add(23)
PS C:\Users\hugo> $ports.Remove(23)
True
PS C:\Users\hugo> # $ports.Add("HTTP")  # Error: no se puede convertir el valor "HTTP" a tipo "System.Int32"
PS C:\Users\hugo> $ports | Sort-Object
53
80
443
```

### 6. Inventario de servicios críticos (Lista[cadena])
```bash
PS C:\Users\hugo> $arr = @("Spooler","W3SVC","LanmanWorkstation")
PS C:\Users\hugo> $services = [System.Collections.Generic.List[string]]::new($arr)
PS C:\Users\hugo> $services.Add("wuauserv")
PS C:\Users\hugo> $services = $services | Sort-Object
PS C:\Users\hugo> foreach ($s in $services) { "Monitorizando servicio: $s... OK" }
Monitorizando servicio: LanmanWorkstation... OK
Monitorizando servicio: Spooler... OK
Monitorizando servicio: W3SVC... OK
Monitorizando servicio: wuauserv... OK
```

## Bloque IV: Manipulación de texto
### 7. Análisis de registro de usuario
```bash
PS C:\Users\hugo> $logLine = " User: admin ; IP: 192.168.1.55 ; Status: Failed "
PS C:\Users\hugo> $clean = $logLine.Trim()
PS C:\Users\hugo> $parts = $clean.Split(";")
PS C:\Users\hugo> $user = $parts[0].Split(":")[1].Trim()
PS C:\Users\hugo> $ip = $parts[1].Split(":")[1].Trim()
PS C:\Users\hugo> "ALERTA: El usuario $user intentó conectarse desde $ip"
ALERTA: El usuario admin intentó conectarse desde 192.168.1.55
```

### 8. Generador de CSV para recursos humanos
```bash
PS C:\Users\hugo> $m1="ana@empresa.com"; $m2="luis@empresa.com"; $m3="bea@empresa.com"
PS C:\Users\hugo> $tmp = @($m1,$m2,$m3)
PS C:\Users\hugo> $csv = $tmp -join ","
PS C:\Users\hugo> "EmailAddress"
EmailAddress
PS C:\Users\hugo> $csv
ana@empresa.com,luis@empresa.com,bea@empresa.com

```
---
[Volver al índice](../../index.md)
