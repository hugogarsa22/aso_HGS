# PR0607: Limpieza de datos de usuarios
---

## Script para generar usuarios_importat.csv que contenga objetos con las columnas de: NombreCompleto, Usuario, Email, Departamento y PassworsInicial.

``` bash
$datosRaw = Get-Content -Path "nuevos_empleados_raw.txt"

$objetosUsuarios = foreach ($linea in $datosRaw) {
    if ($linea.StartsWith(" ")) { continue }

    $partes = $linea -split "\|"

    $bloqueIdentidad = $partes[0].Split(',')
    $apellidosRaw = $bloqueIdentidad[0].Trim()
    $nombreRaw = $bloqueIdentidad[1].Trim()

    $nombreTC = (Get-Culture).TextInfo.ToTitleCase($nombreRaw.ToLower())
    $apellidosTC = (Get-Culture).TextInfo.ToTitleCase($apellidosRaw.ToLower())
    $nombreCompleto = $nombreTC + " " + $apellidosTC

    $userNombre = $nombreRaw.Substring(0,1).ToLower()
    $primerApellido = $apellidosRaw.Split(' ')[0]
    $longitud = $primerApellido.Length
    if ($longitud -gt 6) { $longitud = 6 }
    $userApellido = $primerApellido.Substring(0, $longitud).ToLower()
    $usuarioSAM = $userNombre + $userApellido

    $emailNombre = $nombreRaw.Replace(' ', '.').ToLower()
    $emailApellido = $apellidosRaw.Replace(' ', '.').ToLower()
    $emailFinal = $emailNombre + "." + $emailApellido + "@techiberia.com"

    $departamento = $partes[1].Split('-')[1]

    $anioNacimiento = (Get-Date $partes[2]).Year
    $password = "ChangeMe" + $anioNacimiento + "!"

    [PSCustomObject]@{
        NombreCompleto  = $nombreCompleto
        Usuario         = $usuarioSAM
        Email           = $emailFinal
        Departamento    = $departamento
        PasswordInicial = $password
    }
}

$objetosUsuarios | Export-Csv -Path "usuarios_importar.csv" -NoTypeInformation -Encoding UTF8
$objetosUsuarios | Format-Table -AutoSize
}
```

