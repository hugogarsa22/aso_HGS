# PR0608: Comparación de listas
## Objetivo:

Eres administrador de sistemas Windows. Microsoft acaba de publicar un boletín de seguridad crítico debido a una vulnerabilidad “Zero-Day”.

Tu jefe te ha pasado dos listas en formato texto:

1. La lista oficial de los parches (KBs) que deberían estar instalados para estar protegidos.

 2. La lista real extraída de un servidor crítico (SRV-PRODUCCION) con los parches que tiene instalados actualmente.

Tu objetivo es crear un script que compare ambas listas y te diga exactamente qué parches faltan para poder instalarlos manualmente.

```bash
$kbsRequeridos = @("KB500123", "KB409999", "KB890830", "KB500556", "KB500321", "KB999999")
$kbsInstalados = @("KB100000", "KB500556", "KB409999", "KB100001", "KB890830", "KB200022")

$kbsFaltantes = @()
foreach ($kb in $kbsRequeridos) {
    if ($kbsInstalados -notcontains $kb) {
        $kbsFaltantes += $kb
    }
}

$kbsExtra = @()
foreach ($kb in $kbsInstalados) {
    if ($kbsRequeridos -notcontains $kb) {
        $kbsExtra += $kb
    }
}

$totalRequeridos = $kbsRequeridos.Count
$totalInstalados = $kbsInstalados.Count
$cantidadFaltantes = $kbsFaltantes.Count
$porcentajeCumplimiento = [math]::Round((($totalRequeridos - $cantidadFaltantes) / $totalRequeridos) * 100)

Write-Host "=== AUDITORIA DE SEGURIDAD ==="
Write-Host "Total Requeridos: $totalRequeridos"
Write-Host "Total Instalados: $totalInstalados"
Write-Host ""
Write-Host "ESTADO DE CUMPLIMIENTO: $porcentajeCumplimiento%"
Write-Host ""
Write-Host "[URGENTE] Parches Faltantes:"
Write-Host ($kbsFaltantes -join ", ")
Write-Host ""
Write-Host "[INFO] Parches 'Extra' instalados (No criticos):"
Write-Host ($kbsExtra -join " - ")

```