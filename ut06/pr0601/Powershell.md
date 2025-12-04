# PR0601 – Introducción a PowerShell

## 1. Descubrimiento y ayuda
### 1.1 Búsqueda por nombre (Sustantivo)  
Lista todos los comandos disponibles en el sistema que tengan la palabra **Service** en su nombre (noun).

### 1.2 Búsqueda por acción (Verbo)  
Lista todos los comandos disponibles cuya acción sea **Stop** (detener).

### 1.3 Uso de la ayuda  
Muestra por pantalla la ayuda detallada del comando **Get-Process**, mostrando específicamente los ejemplos de uso.

---

## 2. Exploración de objetos
### 2.1 Introspección de tipos  
Ejecuta el comando **Get-Date** y canaliza su salida a **Get-Member**.  
Responde: ¿Cuál es el **TypeName** del objeto devuelto?

### 2.2 Propiedades vs Métodos  
Usando **Get-Member** sobre un proceso cualquiera (ej: **Get-Process**), identifica el nombre de un **Método** que permita finalizar el proceso.

---

## 3. El Pipeline (selección y ordenación)
### 3.1 Selección de columnas  
Obtén la lista de todos los procesos, mostrando únicamente las propiedades **Id** y **ProcessName**.

### 3.2 Ordenación básica  
Lista todos los procesos del sistema, ordenados por su consumo de **CPU** de forma descendente.

### 3.3 Formato de tabla  
Obtén los servicios del sistema y fuerza la salida para que se muestre como una tabla (**Format-Table**) con **-AutoSize**.

---

## 4. Filtrado y lógica (Where-Object)
### 4.1 Filtrado exacto  
Muestra los servicios cuyo estado (**Status**) sea exactamente igual a “Running”.

### 4.2 Filtrado numérico  
Lista los procesos cuyo identificador (**Id**) sea mayor que 2000.

### 4.3 Filtrado con comodines  
Muestra los procesos cuyo nombre (**Name**) comience por la letra “s” usando **-like** y el comodín adecuado.

---

## 5. Agrupación y estadísticas
### 5.1 Agrupación de datos  
Agrupa todos los servicios del sistema en función de su **Status** y muestra cuántos hay en cada grupo.

### 5.2 Cálculo estadístico  
Obtén el listado de archivos del directorio actual (**Get-ChildItem**) y calcula el **promedio (Average)** de la propiedad **Length**.

---

## 6. Gestión del Historial
### 6.1 Consulta de actividad  
Muestra la lista de los últimos comandos ejecutados en la sesión actual.

### 6.2 Exportación de datos  
Exporta todo tu historial de comandos actual a un archivo en formato **CSV** llamado `historial_lab.csv`.
