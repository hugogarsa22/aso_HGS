# PR0303: Ejercicios sobre los comandos while, until y for
### 1. Contar hasta 10 con for
```bash
#!/bin/bash
for contador in {1..10}
do
        echo "$contador"
done
```
### 2. Sumar los primeros 50 números
```bash
#!/bin/bash
sum=0
for contador in {1..50}
do
  sum=$(( $sum + $contador ))
done
  echo $sum
```
### 3. Tabla de multiplicar
```bash
#!/bin/bash
read -p "dame un numero: " num
for contador in {1..10}
do
  res=$(( $num * $contador ))
  echo $res
done
```
### 4. Imprimir cada letra
```bash
#!/bin/bash
read -p "Introduce una palabra: " palabra
for letra  in $( echo $palabra | grep -o . )
do 
  echo $letra
done
```
### 5. Contar números pares del 1 al 20 con while:
```bash
#!/bin/bash
n=2
while [ $n -le 20 ];
 do
  echo $n
  n=$((n + 2))
done
```
### 6. Suma de dígitos
```bash
#!/bin/bash
read -p "Escribe un número: " num
suma=0
while [ $num -gt 0 ]; 
 do
  digito=$((num % 10))
  suma=$((suma + digito))
  num=$((num / 10))
done
echo "La suma de los dígitos es: $suma"
```
### 7. Cuenta regresiva
```bash
#!/bin/bash
read -p "Escribe un número: " num
until [ $num -lt 0 ]; 
 do
  echo $num
  num=$((num - 1))
done
```
### 8. Imprimir solo archivos .txt
```bash
#!/bin/bash
echo "Escribe el nombre del directorio:"
read directorio
if [ -d "$directorio" ];
        then
for archivo in *;
 do
  if [[ $archivo == *.txt ]];
         then
         echo $archivo
  fi
done
else
```
### 9. Factorial de un número
```bash
#!/bin/bash
read -p "Escribe un número: " num
factorial=1
for ((n=1; n<=num; n++));
 do
  factorial=$((factorial * n))
done
echo "El factorial de $num es: $factorial"
```
### 10. Verificar contraseña
```bash
#!/bin/bash
password="1234"
input=""
until [ "$input" == "$password" ];
 do
  read -sp "Introduce la contraseña: " input
  echo
done
echo "Contraseña correcta"
```