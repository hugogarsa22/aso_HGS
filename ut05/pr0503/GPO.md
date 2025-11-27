# PR0503: GPOs

## Parte I: Configuración de políticas de usuario

### Creación del GPO “Restricciones Alumnos”
Herramientas → Administración de directivas de grupo. Donde vamos a crear la GPO:

![Paso 1](img/1.png)

Con Nombre:

![Paso 2](img/2.png)

Clic derecho en el GPO creado → Editar...

![Paso 3](img/3.png)

Configuración de usuario → Directivas → Plantillas Administrativas → Panel de control → Habilitas la política de Prohibir el acceso al Panel de control y a la configuración del equipo:

![Paso 4](img/4.png)

La habilitamos:

![Paso 5](img/5.png)

Configuración de usuario → Directivas → Plantillas Administrativas → Active Desktop → Active Desktop → Habilitas la política de Tapiz del Escritorio:

![Paso 6](img/6.png)

En Nombre del papel tapiz del escritorio ponemos la ruta de la imagen que queremos poner de fondo de escritorio y en Estilo del papel tapiz seleccionamos Ajustar:

![Paso 7](img/7.png)

Panel de control → Componentes de Windows → Explorador de archivos:

![Paso 8](img/8.png)

En Ocultar estas unidades específicas en Mi PC → en elegir una de las siguientes combinaciones: elegimos Restringir solo las unidades A, B, C y D:

![Paso 9](img/9.png)

### Verificación de usuario
Inicia sesión en el equipo cliente con un usuario alumno (ej. alu_dam_1).  
Ejecuta `gpupdate /force`.  
Verifica que: El fondo de pantalla ha cambiado y no se puede abrir el Panel de Control.

![Paso 10](img/10.png)  
![Paso 11](img/11.png)

---

## Parte II: Políticas de equipo y acceso a recursos

### Política de seguridad (UO Equipos)
Desde el Administrador del Servidor accede a Herramientas → Administración de políticas de grupo, donde generas el GPO asociado a la unidad organizativa _Equipos → Aulas_Informatica:

![Paso 12](img/12.png)

Configuración de Equipo → Directivas → Configuración de Windows → Configuración de Seguridad → Directivas de cuenta → Directiva de Contraseñas:

![Paso 13](img/13.png)

Establecemos la longitud mínima de la contraseña en 8 caracteres:

![Paso 14](img/14.png)

Accede al Administrador del Servidor, entra en la sección Herramientas y abre la consola de administración de políticas de grupo. Desde ahí crea el nuevo GPO y enlázalo con la unidad organizativa _Equipos → Aulas_Informatica:

![Paso 15](img/15.png)

### Mapeo de unidad específica (UO Administración)
Abre el GPO en modo edición y dirígete a Configuración de Usuario → Preferencias → Configuración de Windows → Asignaciones de Unidad. Allí defines una nueva asignación de red apuntando a la ruta \\hugo\share\admin y configuras la letra Z: para dicha unidad.

![Paso 16](img/16.png)  
![Paso 17](img/17.png)

### Verificación de recurso
Inicia sesión con un alumno de informática (ej. alu_dam_1). Verifica que NO tiene la unidad Z:.  
Inicia sesión con un alumno de administración (ej. alu_afi_1). Verifica que SÍ aparece la unidad Z:.

![Paso 18](img/18.png)  
![Paso 19](img/19.png)

---

[Volver al índice](../../index.md)
