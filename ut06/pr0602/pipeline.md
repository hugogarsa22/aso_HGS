# PR0602: El pipeline en Powershell

Realiza las siguientes tareas que se te piden utilizando **Powershell**. Para contestar lo mejor es que hagas una captura de pantalla donde se vea el comando que has introducido y las primeras líneas de la salida de este.

1. El comando `Get-Date` muestra la fecha y hora actual. Muestra por pantalla únicamente el año en que estamos.
``` bash
PS C:\WINDOWS\system32> Get-Date -Format "yyyy"
2025
```
2. Uno de los requisitos de Windows 11 es que es procesador tenga **TPM** habilitado. Powershell dispone del comando `Get-TPM` que nos muestra información sobre este módulo. Muestra por pantalla, en formato tabla, las propiedades `TpmPresent`, `TpmReady`, `TpmEnabled` y `TpmActivated`.

```bash
Get-TPM | Format-Table TpmPresent, TpmReady, TpmEnabled, TpmActivated

```
En los siguientes ejercicios trabajaremos con los ficheros devueltos por el comando `Get-ChildItem C:\Windows\System32`.

3. Muestra por pantalla el número de ficheros y directorios que hay en ese directorio.
```bash
PS C:\WINDOWS\system32> Get-ChildItem  | Measure-Object


Count    : 4960
Average  :
Sum      :
Maximum  :
Minimum  :
Property :
```
4. Los objetos devueltos por el comando anterior tienen una propiedad denominada `Extension`, que indica la extensión del archivo. Calcula el número de ficheros en el directorio que tienen la extensión `.dll`.
```bash
PS C:\WINDOWS\system32> Get-ChildItem | Where-Object {$_.Extension -eq ".dll"} | Measure-Object


Count    : 3631
Average  :
Sum      :
Maximum  :
Minimum  :
Property :
```

5. Muestra los ficheros del directorio con extensión `.exe` que tengan un tamaño superior a 50000 bytes.
```bash


```

6. Muestra los ficheros de este directorio que tengan extensión `.dll`, ordenados por fecha de creación y mostrando únicamente las propiedades de fecha de creación (`CreationTime`), último acceso (`LastAccessTime`) y nombre (`Name`).
```bash

``` 
7. Muestra el tamaño (`Length`) y nombre completo (`FullName`) de todos los ficheros del directorio ordenados por tamaño en sentido descendente.
```bash

```
8. Muestra el tamaño y nombre completo de todos los ficheros del directorio que tengan un tamaño superior a 10MB (10000000 bytes) ordenados por tamaño.
```bash
PS C:\WINDOWS\system32> Get-ChildItem | Where-Object {$_.Length -gt 10000000} | Sort-Object Length | Select-Object Length, FullName

   Length FullName
   ------ --------
 10563584 C:\WINDOWS\system32\wmp.dll
 10577560 C:\WINDOWS\system32\onnxruntime.dll
 12989880 C:\WINDOWS\system32\ntoskrnl.exe
 14022088 C:\WINDOWS\system32\vmms.exe
 17874944 C:\WINDOWS\system32\Windows.UI.Xaml.dll
 19492864 C:\WINDOWS\system32\HologramWorld.dll
 20438440 C:\WINDOWS\system32\amdhip64_6.dll
 21762472 C:\WINDOWS\system32\amdhip64.dll
 24121344 C:\WINDOWS\system32\mshtml.dll
 25260032 C:\WINDOWS\system32\Hydrogen.dll
 26071040 C:\WINDOWS\system32\edgehtml.dll
 27976608 C:\WINDOWS\system32\mfxplugin64_hw.dll
 36242888 C:\WINDOWS\system32\vmfirmwarehcl.dll
 60357040 C:\WINDOWS\system32\OneDriveSetup.exe
105433000 C:\WINDOWS\system32\amd_comgr.dll
110283176 C:\WINDOWS\system32\amd_comgr_2.dll
113353968 C:\WINDOWS\system32\amdxc64.so
215625816 C:\WINDOWS\system32\MRT.exe


```
9. Muestra el tamaño y nombre completo de todos los ficheros del directorio que tengan un tamaño superior a 10MB y extensión `.exe` ordenados por tamaño.
```bash
Ge

```

---
[Volver al índice](../../index.md)