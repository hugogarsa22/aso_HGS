# PR0606: Limpieza de logs 2

---

## Script de PowerShell para el procesamiento de logs de inventario, normalizacion de datos y generacion de un reporte estructurado en formato CSV.

``` bash
$movimientosCrudos = @"
[LOG-OK] SKU:A199 :: 2024.01.10_08:00 :: Item:Smartphone_X :: Qty:50 :: Status:In_Stock
[LOG-ALERT] SKU:B250 :: 10-01-2024 09:15 :: Item:LAPTOP-PRO :: Qty:-5 :: Status:Damaged
[LOG-OK] SKU:C312 :: 2024/01/10_10:30 :: Item:tablet_air :: Qty:120 :: Status:In_Stock
[LOG-CRIT] SKU:D400 :: 11/01/2024_11:45 :: Item:UNKNOWN_ITEM :: Qty:0 :: Status:Out_Of_Order
"@ -split "`r`n"

$objetosProcesados = foreach ($linea in $movimientosCrudos) {
    if ($linea.StartsWith("[LOG-OK]")) { continue }

    $partes = $linea -split " :: "
    
    $nivelRaw = $partes[0].Split(']')[0].Replace('[', '').Trim()
    $sku      = $partes[0].Split(':')[1].Trim()

    $fechaLimpia = $partes[1].Replace('.', '/').Replace('_', ' ')
    $timeStamp   = (Get-Date $fechaLimpia).ToString("dd/MM/yyyy HH:mm")

    $itemRaw = $partes[2].Split(':')[1].Trim().ToUpper()
    if ($itemRaw -eq "UNKNOWN_ITEM") { $itemRaw = "PENDING_REVIEW" }

    $cantidad = $partes[3].Split(':')[1].Trim()
    $estado   = $partes[4].Split(':')[1].Trim()

    $accion = ""
    if ($estado -eq "Damaged") { $accion = "Repair" }
    if ($estado -eq "Out_Of_Order") { $accion = "Replace" }

    [PSCustomObject]@{
        TimeStamp      = $timeStamp
        Severity       = $nivelRaw
        SKU            = $sku
        Item           = $itemRaw
        Qty            = $cantidad
        Status         = $estado
        ActionRequired = $accion
    }
}

$objetosProcesados | Export-Csv -Path "reporte_inventario.csv" -NoTypeInformation -Encoding UTF8
$objetosProcesados | Format-Table -AutoSize
```