# TRABAJO INDIVIDUAL
Michelle Maryan Delgadillo Quiroga

## Clase 1 - Introducción a GIT

### ¿Qué es GIT?

GIT es un Sistema de Control de Versiones Distribuido (VCS). Nos permite guardar archivos y las versiones de estos a lo largo del tiempo de manera local.

### ¿Cómo nació GIT?

Linus Torvalds (creador de Linux) y sus colaboradores usaban BitKeeper para gestionar el código de Linux. BitKeeper les retiró el acceso gratuito, así que Linus decidió crear su propio sistema de control de versiones. En 2 a 3 semanas creó GIT.

### ¿Cómo instalar GIT?

Ir a https://git-scm.com/install/ y seguir los pasos para tu sistema operativo. Para verificar que se instaló correctamente, ejecutar en la terminal: `git --version`

### Configuraciones básicas

Antes de usar GIT hay que configurar tu identidad con los siguientes comandos:

```bash
git config --global user.name "Tu Nombre"
git config --global user.email "tu@correo.com"
git config --global core.autocrlf true
```

### Sistema de calificación

La nota final es sobre 100 puntos. El examen presencial vale 50 pts, el trabajo grupal 30 pts, el trabajo individual 10 pts, la asistencia 9 pts (1 pt por clase) y el form del 19 de abril 1 pt. Hay hasta 10 puntos extra por participación en clase, correcciones o ayuda en la FLISoL. El puntaje mínimo para aprobar es 65/100.

### - Trabajo individual

Cada uno crea su propio repositorio desde el día 1. Debe contener un README.md con el nombre del estudiante y apuntes diarios de cada clase, con commits hechos día a día (no a última hora). Las imágenes van en una carpeta llamada `images/`. Si se falta a una clase hay que avisar al auxi y justificarlo en los apuntes. Entrega hasta el 2 de mayo a las 21:00.

### - Trabajo grupal

Grupos de 4 personas. Se desarrolla un mini proyecto a elección usando GIT Flow y las buenas prácticas vistas en clase. El README.md debe tener el nombre del equipo, los integrantes, una descripción del proyecto y las instrucciones para ejecutarlo. La nota es grupal y se espera participación equitativa de todos. Entrega hasta el 2 de mayo a las 21:00.

### - Archivos que todo repositorio debería tener

README.md describe el proyecto: qué es, quiénes contribuyen y cómo usarlo.

.gitignore lista los archivos y carpetas que GIT debe ignorar, como dependencias o variables de entorno.


## Clase 2 - States y Commits

### Los estados de GIT

Un archivo en GIT pasa por tres estados principales. El Directorio de Trabajo es tu carpeta local donde escribes código, pero GIT aún no lo tiene guardado. El Stage Area es el área de espera donde le dices a GIT qué cambios querés guardar. El Repositorio Local es el historial definitivo, donde tus cambios ya tienen un ID (hash) y son parte de la historia. Desde ahí también se puede sincronizar con un repositorio remoto.

### Directorio de Trabajo (Modificado)

GIT observa todos los archivos de tu carpeta (excepto los que están en el .gitignore) y los cataloga en dos estados: Untracked, que es cuando el archivo es nuevo y GIT nunca lo ha visto antes, y Modified, que es cuando GIT ya tenía una versión previa del archivo y lo modificaste, eliminaste o cambiaste de nombre.

Para revertir un archivo modificado a su estado original se usa:

```bash
git restore <archivo>
```

Cuidado: este comando borra físicamente los cambios que hiciste.

Para que GIT ignore un archivo nuevo, simplemente hay que agregar su nombre completo al `.gitignore`.

### Stage Area (Preparado)

El stage area permite elegir qué archivos modificados se incluirán en el próximo commit. Para agregar archivos al stage:

```bash
git add <archivo>   # agrega un archivo específico
git add .           # agrega todos los archivos observados por GIT
```

Para sacar un archivo del stage y volver al estado anterior:

```bash
git restore --staged <archivo>
```

### Repositorio Local (Confirmado)

Esta es la fase final. El commit crea un punto de guardado en el historial con todos los cambios que estaban en el stage area.

```bash
git commit -m "mensaje"
```

Para deshacer el último commit sin perder los cambios:

```bash
git reset --soft HEAD~1
```

### Buenas prácticas en commits

### - ¿Cada cuánto hacer un commit?

Se usan los commits atómicos: cada commit representa un único cambio lógico, pequeño y completo. Es mejor hacer commits pequeños y frecuentes que uno gigante con todo. Eso sí, cada commit debe tener sentido y no dejar el proyecto sin funcionar.

### - Cómo escribir buenos mensajes de commit

El mensaje debe ser corto, claro y en inglés. Las reglas principales son usar verbos imperativos (Add, Change, Fix, Remove), no usar punto final ni puntos suspensivos, y no superar los 50 caracteres. Si necesitás dar más contexto, usá el cuerpo del commit con `git commit` sin el `-m`.

El formato recomendado es:

```bash
git commit -m "<tipo>: <descripción>"
```

### - Prefijos para commits semánticos

`feat` para una nueva característica, `fix` para corregir un bug, `perf` para mejoras de rendimiento, `build` para cambios en el sistema de build, `ci` para integración continua, `docs` para documentación, `refactor` para reestructuración de código, `style` para cambios de formato que no afectan al usuario, y `test` para pruebas.