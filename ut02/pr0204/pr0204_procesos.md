# PR0204: Gestion de procesos en Linux
## Pasos 
### 1
Se abrió una terminal en el sistema Linux y se ejecutó el comando ps para listar los procesos asociados al usuario actual. Se anotaron los PID de al menos tres procesos.
Tuve que añadir un proceso para que hubiera al menos tres.

``` bash
HGS_ssh@HGSserver:~$ ps
    PID TTY          TIME CMD
   1491 pts/0    00:00:00 bash
   1529 pts/0    00:00:00 sleep
   1530 pts/0    00:00:00 ps
HGS_ssh@HGSserver:~$

```

Se utilizó el comando ps aux para listar todos los procesos del sistema. Se identificó y anotó el PID de un proceso que no pertenecía al usuario actual.

```bash
message+     715  0.0  0.1   9784  5376 ?        Ss   07:24   0:00 @dbus-daemon --system --address
```

¿Qué diferencia hay entre ps y ps aux? 

El comando ps te muestra solo los procesos que tú estás ejecutando en ese momento desde tu terminal. Es como mirar lo que tienes abierto tú mismo. En cambio, ps aux te enseña todos los procesos que están corriendo en el sistema, aunque los haya iniciado otro usuario o no estén conectados a ninguna terminal. Es como ver todo lo que está pasando en el ordenador, no solo lo tuyo.

¿Qué implica que un proceso pertenezca a un usuario?

Cuando decimos que un proceso pertenece a un usuario, significa que ese usuario fue quien lo lanzó. Eso afecta a qué puede hacer ese proceso: solo podrá acceder a los archivos y permisos que tenga ese usuario. Además, solo ese usuario (o el administrador) puede pararlo, cambiarle la prioridad o mandarle señales. Es una forma de mantener el sistema organizado y seguro, para que cada uno tenga control sobre lo suyo y no se meta en lo de los demás.
### 2
Se ejecutó el comando top para monitorizar los procesos en tiempo real. Se identificó el proceso que consumía más CPU y se anotó su PID.

```bash
   PID USER      PR  NI    VIRT    RES    SHR S  %CPU  %MEM     TIME+ COMMAND
   1537 HGS_ssh   20   0   11904   5888   3712 R   4,8   0,1   0:00.12 top
```
Se presionó la tecla M dentro de top para ordenar los procesos por uso de memoria. Se anotó el nombre del proceso que más memoria consumía.


![alt text](procesomemoria.png)

¿Qué columnas aparecen en top y qué significan? 

Cuando usas el comando top, te sale una lista con todos los procesos que están funcionando en ese momento. Cada fila representa un proceso, y cada columna te da información sobre él. Por ejemplo:
``` bash
PID es el número que identifica al proceso.

USER te dice qué usuario lo lanzó.

%CPU muestra cuánta CPU está usando.

%MEM indica cuánta memoria RAM está consumiendo.

COMMAND es el nombre del programa o comando que se está ejecutando.

```
Con esto puedes ver fácilmente qué está usando más recursos y quién lo está ejecutando.

¿Cómo se cambia el tiempo de actualización en top? 

Por defecto, top se actualiza cada pocos segundos. Si quieres cambiar ese ritmo, solo tienes que pulsar la tecla d mientras estás dentro de top. Te pedirá que pongas un número, que será el nuevo intervalo en segundos. Por ejemplo, si pones 1, se actualizará cada segundo.

### 3
