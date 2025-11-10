# PR0302: Comando case
### 1: Menú de operaciones matemáticas 
```bash
#!/bin/bash
read -p "Introduce el pimer numero: " num1
read -p "Introduce el segundo numero: " num2
read -p "Introduce la operacion que quieras hacer: " operacion
case $operacion in
        suma)
                resultado=$(expr $num1 + $num2)
                echo "El resultado es $resultado";;
        resta)
                resultado=$(expr $num1 - $num2)
                echo "El resultado es $resultado";;
        multi)
                resultado=$(expr $num1 \* $num2)
                echo "El resultado es $resultado";;
        dividir)
                resultado=$(expr $num1 / $num2)
                echo "El resultado es $resultado";;
esac
```
### 2: Identificar el tipo de archivo 
```bash
#!/bin/bash
read -p "Introduce la extension de un archivo: " ext
case $ext in
        .txt)
           echo "Texto";;
        .png | .jpg | .psd | .clip)
            echo "Imagen";;
        .pdf)
            echo "Documento";;
        .mp4 | .mkv | .wav)
            echo "Video";;
esac
```
### 3: Conversión de unidades de longitud
```bash
#!/bin/bash
read -p "Introduce los metros: " num
read -p "¿A que quieres pasarlo? KM, CM o MM: " op
case $op in
       [Kk][Mm])
               resultado=$(( $num / 1000 ))
                echo "El resultado es $resultado";;
        [Cc][Mm])
               resultado=$(( $num * 100 ))
                echo "El resultado es $resultado";;
        [Mm][Mm])
               resultado=$(( $num * 1000 ))
                echo "El resultado es $resultado";;
esac
```
### 4: Menu de cofiguracion del sistema
```bash
#!/bin/bash
read -p "¿Qué deseas hacer? Apagar, Reiniciar o Salir: " op
case $op in
       [Aa][Pp][Aa][Gg][Aa][Rr])
               echo "Apagando el sistema..."
               shutdown -h now
               ;;
       [Rr][Ee][Ii][Nn][Ii][Cc][Ii][Aa][Rr])
               echo "Reiniciando el sistema..."
               reboot
               ;;
       [Ss][Aa][Ll][Ii][Rr])
               echo "Cerrando sesión..."
               kill -9 -1
               ;;
esac
```
### 5:Dia de la semana
```bash
#!/bin/bash
read -p "Introduce un número entre 1 y 7: " dia_num

case $dia_num in
    1)
        echo "Lunes"
        ;;
    2)
        echo "Martes"
        ;;
    3)
        echo "Miércoles"
        ;;
    4)
        echo "Jueves"
        ;;
    5)
        echo "Viernes"
        ;;
    6)
        echo "Sábado"
        ;;
    7)
        echo "Domingo"
        ;;
    *)
        echo "Error: El número introducido no está entre 1 y 7."
        ;;
esac

exit 0
```
### 6: Clasificar calificaciones 
```bash
#!/bin/bash
read -p "Introduce una nota " nota
case $nota in
        [0-4])
           echo "$nota es suspenso";;
        5)
            echo "$nota es suficiente";;
        6)
            echo "$nota es bien";;
        7 | 8)
            echo "$nota es notable";;
        9 | 10)
            echo "$nota es sobresaliente";;
esac
```

### 7: Clasificar numero 
```bash
#!/bin/bash
read -p "Introduce un número: " num

case $num in
    -*)
        echo "Negativo"
        ;;
    0)
        echo "Cero"
        ;;
    [1-9]* | +*)
        echo "Positivo"
        ;;
    *)
        echo "Error: Entrada no válida."
        ;;
esac

exit 0
```
### 8: Control servicios 
```bash
#!/bin/bash
read -p "Introduce el nombre del servicio: " serv
read -p "¿Que quieres hacer con el servicio? (iniciar, detener, reiniciar): " acc

status=0

case $acc in
    iniciar)
        systemctl start $serv > /dev/null 2>&1
        status=$?
        ;;
    detener)
        systemctl stop $serv > /dev/null 2>&1
        status=$?
        ;;
    reiniciar)
        systemctl restart $serv > /dev/null 2>&1
        status=$?
        ;;
    *)
        echo "Error: Acción no válida. Introduce 'iniciar', 'detener' o 'reiniciar'."
        status=127
        ;;
esac

if [ $status -eq 0 ]
then
    echo "Operación '$acc' sobre el servicio '$serv' realizada correctamente."
else
    if [ $status -eq 127 ]
    then
        echo "La acción '$acc' no es una opción válida."
    else
        echo "Error: No se pudo completar la operación '$acc' sobre el servicio '$serv'."
        echo "Comprueba si el servicio existe o si tienes permisos."
    fi
fi

exit $status

```