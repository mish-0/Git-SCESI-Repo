# TRABAJO INDIVIDUAL
Michelle Maryan Delgadillo Quiroga

## Clase 1 - Introducción a GIT

### ¿Qué es GIT?

GIT es básicamente una herramienta que te permite guardar el historial de cambios de tus archivos con el tiempo, todo de forma local en tu computadora. Se lo conoce como un Sistema de Control de Versiones Distribuido, o VCS por sus siglas en inglés.

### ¿Cómo nació GIT?

La historia es bastante curiosa. Linus Torvalds, el que creó Linux, usaba junto a su equipo una herramienta llamada BitKeeper para manejar el código. En algún momento BitKeeper les quitó el acceso gratuito, y Linus simplemente decidió hacer su propia herramienta. En unas 2 o 3 semanas ya tenía GIT funcionando, lo cual es una locura.

### ¿Cómo instalar GIT?

Hay que entrar a https://git-scm.com/install/ y descargar el instalador según tu sistema operativo. Una vez instalado, para confirmar que quedó bien debes abrir la terminal y escribir:

```bash
git --version
```

Si te muestra un número de versión, está todo bien.

### Configuraciones básicas

Lo primero antes de empezar a usar GIT es decirle quién eres, porque esa información aparece en cada commit que haces:

```bash
git config --global user.name "Tu Nombre"
git config --global user.email "tu@correo.com"
git config --global core.autocrlf true
```

### Sistema de calificación

El curso se aprueba con 65 puntos sobre 100. La mayor parte de la nota viene del examen presencial (50 pts), después el trabajo grupal vale 30 pts, el individual 10 pts, la asistencia 9 pts a razón de 1 por clase, y el form del 19 de abril suma 1 pt. Además hay hasta 10 puntos extra por participar en clase o colaborar en la FLISoL.

### - Trabajo individual

Hay que crear el repositorio desde el primer día e ir agregando apuntes de cada clase con commits diarios, no todo junto al final porque el auxi revisa las fechas. El README.md tiene que tener el nombre propio y las notas de cada clase. Si se usan imágenes, van en una carpeta llamada `images/`. Entrega el 2 de mayo a las 21:00.

### - Trabajo grupal

Se forman grupos de 4 y se hace un mini proyecto a elección. Tiene que usar GIT Flow y las buenas prácticas del curso. El README.md debe explicar bien el proyecto e incluir instrucciones para que el auxi pueda ejecutarlo. Todos deben participar por igual. Entrega el 2 de mayo a las 21:00.

### Archivos que todo repositorio debería tener

El README.md es la cara del proyecto, lo primero que ve cualquiera que entra al repo, así que tiene que explicar bien de qué trata y cómo usarlo.

El .gitignore le dice a GIT qué archivos ignorar, por ejemplo carpetas de dependencias o archivos con contraseñas que no deberían subirse nunca.

## Clase 2 - States y Commits

### Los estados de GIT

En GIT los archivos pasan por tres zonas. Primero están en el Directorio de Trabajo, que es básicamente tu carpeta normal donde escribes código. Después los mandas al Stage Area, que vendría a ser como una sala de espera donde eliges qué cambios van a entrar al siguiente guardado. Y finalmente haces el commit, que los manda al Repositorio Local y ya quedan registrados en el historial con un ID único llamado hash. También existe el repositorio remoto (como GitHub) al que se sincronizan los cambios desde el local.

### Directorio de Trabajo

Dentro del directorio de trabajo, GIT clasifica los archivos en dos: Untracked son los archivos nuevos que GIT nunca antes había visto, y Modified son los que GIT ya conocía pero que cambiaste, borraste o renombraste.

Si metiste la pata y quieres que un archivo vuelva a como estaba antes de modificarlo:

```bash
git restore <archivo>
```

Ojo con este, porque borra los cambios para siempre, no hay vuelta atrás.

Si hay un archivo que no quieres que GIT vea para nada, lo agregas al `.gitignore` con su nombre completo y listo.

### Stage Area

Acá es donde eliges qué va y qué no va en el próximo commit. No tienes que guardar todo junto si no quieres.

```bash
git add <archivo>   # agrega un archivo específico
git add .           # agrega todo de una
```

Si te arrepientes y quieres sacar algo del stage sin perder tus cambios:

```bash
git restore --staged <archivo>
```

### Repositorio Local

Una vez que tienes todo lo que quieres en el stage, haces el commit para grabarlo en el historial:

```bash
git commit -m "mensaje"
```

Si el último commit estuvo mal y quieres deshacerlo pero sin perder lo que escribiste:

```bash
git reset --soft HEAD~1
```

### Buenas prácticas en commits

### - ¿Cada cuánto hacer un commit?

La idea es hacer commits atómicos: pequeños, frecuentes y que cada uno represente un solo cambio con sentido. Nada de acumular todo el día y hacer un commit gigante al final. Pero tampoco hacer commits al azar sin que signifiquen nada. Cada commit debería dejar el proyecto funcionando.

### - Cómo escribir el mensaje

Tiene que ser en inglés, con verbo imperativo al inicio (Add, Fix, Change, Remove), sin punto al final y máximo 50 caracteres. Si necesitas explicar más, usas `git commit` solo (sin `-m`) y en el cuerpo del mensaje escribes el detalle.

El formato que se usa es:

```bash
git commit -m "<tipo>: <descripción>"
```

### - Prefijos

`feat` para algo nuevo, `fix` para corregir un bug, `docs` para documentación, `style` para cambios de formato que no afectan el funcionamiento, `refactor` para reorganizar código, `perf` para mejorar rendimiento, `test` para pruebas, `build` para el sistema de build y `ci` para integración continua.

## Clase 3 - GitHub y SSH

### ¿Qué es GitHub?

GitHub es como una red social para desarrolladores pero enfocada en código. Básicamente es un servidor en la nube donde puedes subir tus repositorios de GIT para que otros los vean, y también para colaborar en proyectos de otras personas.

### Git vs GitHub

Son cosas distintas aunque suenen parecido. GIT es la herramienta que corre en tu computadora y maneja el historial de cambios. GitHub es la plataforma donde ese historial se sube y se comparte. GitHub usa GIT por debajo, pero no son lo mismo.

### SSH vs HTTPS

Para conectarte a GitHub desde tu computadora tienes dos opciones. Con HTTPS te va a pedir contraseña o token cada vez que haces un push, lo cual es bastante molesto. Con SSH configuras una clave en tu PC que GitHub ya reconoce, así nunca más te pide autenticarte. La recomendación es siempre usar SSH.

### Cómo configurar SSH

Desde la terminal (Git Bash si estás en Windows, terminal normal en Linux) ejecutas:

```bash
ssh-keygen -t ed25519 -C "tu-correo@email.com"
```

Eso genera tu clave. Para verla y copiarla:

```bash
cat ~/.ssh/id_ed25519.pub
```

Con ese contenido copiado, vas a GitHub → tu perfil → Settings → SSH and GPG Keys → New SSH Key, le pones un nombre, pegas la clave y guardas. Para verificar que quedó bien:

```bash
ssh -T git@github.com
```

### Crear un repositorio en GitHub

Vas a tu perfil en GitHub, entras a la pestaña de repositorios y clickeas en "New". Le pones nombre, opcionalmente una descripción, y creas el repositorio.

### Conectar un repo local con GitHub

Si ya tienes un repo local inicializado y con al menos un commit, podés vincularlo a GitHub con:

```bash
git remote add origin git@github.com:TuUser/TuRepo.git
git branch -M main
git push -u origin main
```

`origin` es simplemente el apodo que GIT le da por defecto a la URL del repositorio remoto. Se puede cambiar pero por convención se deja así.

### Clonar un repositorio

Para bajarte un repo de GitHub a tu máquina:

```bash
git clone git@github.com:TuUser/TuRepo.git
```

Si por error lo clonaste con HTTPS y quieres pasarlo a SSH para no tener que autenticarte cada vez:

```bash
git remote set-url origin git@github.com:TuUser/TuRepo.git
```

Este mismo comando sirve también si quieres apuntar el repo local a otro repositorio remoto distinto. Para ver a qué remoto está conectado tu repo:

```bash
git remote -v
```

### Subir y bajar cambios

Para subir tus commits al repositorio remoto:

```bash
git push origin <rama>
```

Para traer los cambios que alguien más subió (o los que subiste desde otra PC):

```bash
git pull origin <rama>
```