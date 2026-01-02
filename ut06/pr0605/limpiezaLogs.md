# PR0605: Limpieza de logs

---

## Objetivo: Tienes un texto desordenado con registros del servidor. Debes crear un script que limpie esos datos, normalice las fechas, corrija los nombres de usuario y guarde todo en un archivo CSV ordenado, ignorando los mensajes informativos.

 ```bash
$logCrudo = @"
[INFO] ID:8842 :: 2023/11/01_10:00 :: User:admin_01 :: Action:Login_Success
[ERROR] ID:9921 :: 2023/11/01_10:05 :: User:guest_user :: Action:Auth_Fail (Pass)
[WARN] ID:8843 :: 2023-11-01 10:15 :: User:dev_team :: Action:Upload_Limit_Exceeded
[CRITICAL] ID:1001 :: 01-11-2023_10:20 :: User:ROOT :: Action:Service_Stop
"@

$informe = New-Object System.Collections.Generic.List[PSCustomObject]
$lineas = $logCrudo.Split("`n")

foreach ($linea in $lineas) {
    $l = $linea.Trim()

    if ($l.Length -eq 0 -or $l -match "\[INFO\]") {
        continue
    }

    $partes = $l -split "::"

    $bloqueInfo = $partes[0].Trim()
    $infoSplit = $bloqueInfo.Split(" ") 
    $severity = $infoSplit[0].Replace("[", "").Replace("]", "")
    $eventID = $infoSplit[1].Replace("ID:", "")

    $fechaRaw = $partes[1].Trim()
    $fechaLimpia = $fechaRaw.Replace("_", " ").Replace("/", "-").Replace(".", "-")
    $fechaObj = [datetime]$fechaLimpia
    $fechaFinal = $fechaObj.ToString("yyyy-MM-dd HH:mm")

    $userLimpio = $partes[2].Replace("User:", "").Trim().ToLower()

    if ($userLimpio -eq "root") {
        $userFinal = "administrator"
    } else {
        $userFinal = $userLimpio
    }

    $actionFinal = $partes[3].Replace("Action:", "").Trim()

    $fila = [PSCustomObject]@{
        TimeStamp = $fechaFinal
        Severity  = $severity
        User      = $userFinal
        EventID   = $eventID
        Action    = $actionFinal
    }

    $informe.Add($fila)
}

$informe | Export-Csv "reporte_seguridad.csv" -NoTypeInformation -Encoding UTF8
```


### Explicacion del código:

La Lista (New-Object...List): Creamos una "caja vacía" eficiente. Usamos una lista en vez de un array normal porque es mucho más rápida para ir metiendo datos uno a uno sin bloquearse.

El Filtro (continue): Revisamos línea por línea. Si la línea dice [INFO], usamos el comando continue. Esto le dice al script: "Ignora esto y pasa inmediatamente a la siguiente línea", así no perdemos tiempo procesando basura.

Cortar y Limpiar (Split y Replace):

Usamos Split ("cortar") para separar la línea cada vez que aparecen los dos puntos ::.

Usamos Replace ("reemplazar") para borrar la suciedad, como los corchetes [] o cambiar los guiones bajos _ de la fecha por espacios.

La Ficha (PSCustomObject): Una vez tenemos los datos limpios (fecha, usuario, error), creamos una "ficha" ordenada con esos datos. Esto es lo que permite que al final, al exportar, salga una tabla perfecta en el Excel (CSV) y no un texto plano.