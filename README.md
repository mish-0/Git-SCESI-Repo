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

Si ya tienes un repo local inicializado y con al menos un commit, puedes vincularlo a GitHub con:

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

## Clase 4 - Remote, SSH Múltiple y Checkout

### git remote

`git remote` es el comando para gestionar a dónde apunta tu repo local cuando quieres enviar o recibir cambios. Lo más útil que puedes hacer con él es ver la URL actual, vincular un repo nuevo o cambiar la URL si te equivocaste.

```bash
git remote -v                          # muestra a dónde apunta
git remote add <apodo> "url"           # vincula con un repo remoto
git remote set-url <apodo> "url"       # cambia la URL
```

### Múltiples SSH

Si tienes más de una cuenta de GitHub, necesitas una clave SSH distinta para cada una. La idea es que cada cuenta tenga su propio "túnel" de acceso, porque si usas la misma llave para todo, las cuentas se confunden entre sí.

### Cómo configurar múltiples SSH

Primero generas la nueva clave con un nombre diferente para no pisar la que ya tienes:

```bash
ssh-keygen -t ed25519 -C "micorreo@gmail.com" -f ~/.ssh/id_miname
```

Después creas un archivo `config` dentro de `~/.ssh/` para que GIT sepa qué llave usar para cada cuenta:

```
# Cuenta personal
Host github.com
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_ed25519

# Segunda cuenta
Host github-miname
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_miname
```

Para verificar que funciona:

```bash
ssh -T git@github-miname
```

Cada campo del config sirve para algo específico. `Host` es el apodo que le pones a esa conexión, el que escribes después de `git@`. `HostName` es la dirección real del servidor, que siempre va a ser `github.com`. `User` es siempre `git` para GitHub. `IdentityFile` es la ruta a la llave privada que corresponde a ese host.

Importante: si clonas un repo con la segunda cuenta, tienes que usar el alias que definiste en el config, no el dominio normal:

```bash
git clone git@github-miname:usuario/repo.git
```

### Configuraciones locales

Las configuraciones que hicimos en la clase 1 con `--global` aplican para todos los repos de tu computadora. Pero si necesitas usar otro nombre o correo solo en un repo específico, puedes hacer una configuración local que pisa a la global sin tocarla:

```bash
git config user.name "Otro Nombre"
git config user.email "otro@correo.com"
```

La diferencia es simplemente que no lleva el flag `--global`, y solo afecta al repo donde estés parado.

### Git Checkout

`git checkout` mueve el HEAD, que vendría a ser el puntero que indica en qué punto del historial estás parado. Sirve para varias cosas: revisar cómo era el código en un commit viejo, recuperar algo que borraste, probar cosas sin tocar la rama principal, o simplemente cambiar de rama.

### Detached HEAD

Normalmente el HEAD apunta a una rama, que va avanzando cada vez que haces un commit. Pero cuando haces checkout a un commit específico, el HEAD queda apuntando directo a ese commit, suelto, sin rama. A eso se le llama estado "Detached HEAD". Es como estar de visita en el pasado: puedes ver todo, incluso hacer cambios, pero si te vas sin crear una rama nueva, lo que hiciste desaparece.

### Cómo moverse entre commits

Para ir a un commit antiguo necesitas su hash (lo ves con `git log`):

```bash
git checkout <hash_antiguo>
```

Para volver al presente:

```bash
git checkout <rama>
```

Si mientras estabas en Detached HEAD hiciste algún commit y no quieres perderlo, tienes que crear una rama nueva antes de volver:

```bash
git checkout <hash_del_commit_nuevo>
git checkout -b rama_nueva
```

### Buenas prácticas con checkout

Antes de hacer checkout a un commit viejo, asegurate de tener todo commiteado. Si tienes cambios sin guardar GIT no te va a dejar moverte. Tampoco conviene quedarse mucho tiempo en Detached HEAD haciendo cambios; si vas a trabajar en serio, mejor crea una rama desde el principio. Por otro lado, es una herramienta muy útil para estudiar proyectos grandes y ver cómo fueron creciendo commit a commit.

## Clase 5 - Ramas y GitFlow Básico

### Actualización del sistema de calificación

El auxi actualizó algunos puntos del sistema de notas. Ahora el README propio vale 5 pts por separado, la asistencia bajó a 8 pts (sigue siendo 1 pt por clase), y el form del 19 de abril subió a 2 pts. La entrega del trabajo individual también cambió: ahora es el viernes 1 de mayo hasta las 21:30.

### ¿Qué son las ramas?

Una rama es básicamente una línea de desarrollo paralela. Cuando creas una rama, estás partiendo desde el estado actual del código y trabajando en un camino separado sin afectar el resto. Es como tener una copia del proyecto donde puedes hacer cambios tranquilo, y después decides si esos cambios se unen al código principal o no.

### git branch

Con `git branch` puedes gestionar todas las ramas de tu repo.

```bash
git branch              # lista todas las ramas y muestra en cuál estás
git branch <rama>       # crea una rama nueva desde donde estás parado
git branch -D <rama>    # borra una rama
```

### git checkout y git switch con ramas

Ya vimos `git checkout` para moverse entre commits. También funciona para ramas:

```bash
git checkout <rama>      # te mueves a esa rama
git checkout -b <rama>   # crea la rama y te mueves a ella en un solo paso
```

Eso sí, para cambiar de rama no puedes tener archivos en modified, untracked o staged sin commitear.

En 2019 con Git 2.23 introdujeron `git switch`, que hace lo mismo pero solo para ramas, sin el riesgo de terminar en Detached HEAD por error. `git checkout` sigue siendo el clásico que sirve para todo (ramas, commits, archivos), mientras que `git switch` es más específico y seguro para moverse entre ramas.

### GitFlow básico

GitFlow es una forma ordenada de organizar las ramas de un proyecto. Sin una convención así, cada uno nombra sus ramas como quiere y el historial se vuelve un caos. Con GitFlow todos saben qué tipo de trabajo va en qué rama.

### Cómo funciona GitFlow

Hay dos ramas principales que viven para siempre en el proyecto. `main` contiene el código en producción, lo que está funcionando para los usuarios. `develop` es donde se concentra el trabajo del día a día, las cosas que están casi listas pero todavía no se lanzan a producción.

Después están las ramas de apoyo, que nacen y mueren según se necesiten.

`feature/*` se usa cuando vas a trabajar en algo nuevo. Nace de `develop` y cuando terminas, se fusiona de vuelta en `develop` y se elimina. Por ejemplo: `feature/add-search-bar` o `feature/new-form-user`.

`release/*` se usa cuando ya tienes algo listo para lanzar y quieres hacer las pruebas finales antes de subirlo a producción. Nace de `develop` y se fusiona en `main` y `develop`. Por ejemplo: `release/v1.0.0`.

`hotfix/*` es para emergencias: un bug en producción que hay que arreglar ya. Nace desde `main` (no desde `develop`, porque `develop` puede tener cosas inestables) y se fusiona en `main` y `develop`. Por ejemplo: `hotfix/login-authentication-error`.

### Resumen rápido

| Rama | Nace de | Muere en | Para qué |
|---|---|---|---|
| develop | main | nunca | trabajo del día a día |
| feature/* | develop | develop | una tarea específica |
| release/* | develop | main y develop | pulir la versión final |
| hotfix/* | main | main y develop | arreglar algo en producción |

## Clase 6 - Merge, Fetch, Pull, Push y Flujo de Trabajo

### git merge

Merge significa fusión. Este comando une dos ramas en una sola, combinando todos los commits de ambas. Se usa cuando ya terminaste de trabajar en una rama y quieres incorporar esos cambios a otra, por ejemplo de `feature/algo` hacia `develop`.

Se recomienda siempre usar el flag `--no-ff` (no fast forward), que obliga a GIT a crear un commit de merge aunque no sea necesario. Esto sirve para que el historial conserve la trayectoria de la rama aunque después la borres.

```bash
git merge --no-ff <rama>
```

### git fetch

`git fetch` revisa si hubo cambios en el repositorio remoto y sus ramas, pero sin traer nada todavía. Es como asomarse a ver si hay algo nuevo antes de descargarlo. Útil para saber si alguien más hizo cambios antes de ponerse a trabajar.

```bash
git fetch
```

### git pull

`git pull` sí trae los cambios del repositorio remoto y los aplica en tu rama local. Siempre conviene usarlo con `origin` y el nombre de la rama para evitar problemas.

```bash
git pull origin <rama>
```

### git push

`git push` sube tus commits locales al repositorio remoto. Igual que el pull, se usa con `origin` y el nombre de la rama.

```bash
git push origin <rama>
```

Si la rama que estás subiendo es nueva y no existe todavía en el remoto, la primera vez hay que usar el flag `-u` para que GIT la cree en el servidor:

```bash
git push origin -u <rama>
```

### Flujo de trabajo sin Pull Requests

Este es el flujo que se usa para fusionar una rama de trabajo en `develop` de forma ordenada:

```bash
git checkout develop               # te mueves a develop
git fetch                          # revisas si hubo cambios remotos
git pull origin develop            # traes los cambios más recientes
git merge --no-ff <rama>           # fusionas tu rama en develop
# si hay conflictos, los resuelves manualmente en los archivos marcados
git add .                          # añades los archivos resueltos
git commit                         # abres el editor para el mensaje del merge commit
# guardas con Ctrl+O, Enter, Ctrl+X si es nano, o :wq si es vim
git branch -D <rama>               # borras la rama ya fusionada
git push origin develop            # subes develop actualizado al remoto
```

## Clase 7 - Pull Requests y Contribución Open Source

### ¿Qué es un Pull Request?

Un Pull Request (PR) es la forma profesional de proponer cambios en un repositorio. En vez de fusionar directamente tu rama al código base, creas una solicitud en GitHub donde el equipo puede ver exactamente qué cambios quieres meter, discutirlos, pedir modificaciones y aprobarlos o rechazarlos antes de que toquen el código principal.

### ¿Por qué usar PRs si podemos trabajar sin ellos?

Porque sin PRs cualquier colaborador puede pushear y mergear lo que quiera sin avisar a nadie. Eso es un riesgo enorme: ¿y si lo hace mal?, ¿y si está metiendo código malicioso?, ¿y si un colaborador de confianza resulta ser alguien con malas intenciones? Los PRs obligan al equipo a revisar los cambios antes de que entren al proyecto, permiten debatir, opinar, oponerse, y en general dan un mejor control sobre lo que se está poniendo en producción.

### ¿Cómo crear un PR?

Una vez que hiciste `git push origin <rama>`, vas a GitHub y seguís estos pasos:

1. Entras a tu repositorio en GitHub y te mueves a tu rama.
2. GitHub te va a mostrar un botón que dice "Compare & pull request", aparece en los primeros minutos después de subir cambios. Si no aparece, vas a "Contribute" → "Open Pull Request".
3. En la pantalla que se abre, del lado izquierdo eliges la rama a la que quieres hacer merge (por ejemplo `develop` si estás con GitFlow), y del lado derecho está tu rama con los cambios.
4. Pones un título descriptivo. Puedes dejar el del último commit o escribir uno propio que explique bien qué hiciste.
5. En la descripción abajo puedes detallar qué cambios hiciste y por qué.
6. GitHub te muestra los commits incluidos y una vista previa de cómo va a quedar el merge.
7. Clickeas "Create Pull Request".
8. A partir de ahí esperas a que tus compañeros revisen y aprueben. Una vez que se alcanza la cantidad de aprobaciones requeridas, aparece el botón "Merge Pull Request" y cualquiera de los aprobadores puede ejecutarlo.

### ¿Cómo proteger el repositorio y limitar la colaboración?

Saber de PRs no es suficiente si los colaboradores igual pueden mergear sin esperar aprobación. Para forzar que nadie pueda fusionar sin review, hay que configurar un ruleset en GitHub. Los pasos son:

1. Vas a tu repositorio en GitHub → **Settings** → **Branches**.
2. Clickeas en **Add branch ruleset** y le pones un nombre descriptivo, por ejemplo `pull-request-flow-ruleset`.
3. En el estado lo dejas en **Active**.
4. En **Target branches** agregas las ramas que querés proteger. Con GitFlow lo mínimo es proteger `main` y `develop`, porque son las ramas principales a las que nadie debería mergear directamente.
5. En las reglas activás estas dos como mínimo: **Restrict updates** (evita problemas de actualizaciones directas) y **Require a pull request before merging** (obliga a que cualquier cambio pase por un PR antes de entrar a esas ramas).
6. En **Bypass list** lo dejas vacío para que las reglas apliquen a todos, incluyendo al dueño del repo.
7. En **Required approvals** ponés cuántas aprobaciones se necesitan para poder mergear. Se recomienda la mitad más uno del equipo. Si son 4 integrantes, pones 3.
8. Activas también la opción que obliga a re-aprobar si alguien hace un push de último momento después de que el PR ya fue aprobado, para que no puedan meter cambios a escondidas justo antes del merge.
9. Guardas con **Save changes** y listo.

### Flujo de trabajo con Pull Requests

```bash
git checkout develop
git fetch
git pull origin develop
git checkout <rama>              # agregas -b si estás creando la rama
git merge develop               # solo si hubo cambios en develop mientras trabajabas

# trabajas en tu rama, haces tus commits...

git push origin <rama>          # agregas -u si es la primera vez que subes esa rama

# antes de abrir la PR, actualizas tu rama por si develop tuvo cambios nuevos:
git checkout develop
git fetch
git checkout <rama>
git merge develop               # resuelves conflictos si los hay
git add .
git commit                      # guardas con Ctrl+O, Enter, Ctrl+X (nano) o :wq (vim)
git push origin <rama>

# ahora sí abres la PR desde GitHub siguiendo el flujo del video
```

### ¿Cómo contribuir a un proyecto sin ser colaborador invitado?

Esto se hace a través de un Fork. André lo demostró en clase contribuyendo a un repositorio donde no estaba invitado. El proceso es:

Primero haces un fork del repositorio desde GitHub, lo que crea una copia del repo en tu propia cuenta. Después lo clonas a tu computadora:

```bash
git clone https://github.com/tu-usuario/nombre-repo.git
cd nombre-repo
```

Creas una rama para tu cambio, nunca trabajas directo en main:

```bash
git checkout -b docs/mi-cambio
```

Haces tus modificaciones, las commiteas y las subes a tu fork:

```bash
git add .
git commit -m "docs: descripción del cambio"
git push -u origin docs/mi-cambio
```

Finalmente desde GitHub abres un Pull Request desde tu fork hacia el repositorio original, y los dueños del proyecto deciden si lo aceptan o no.


## Clase 8 - Git Diff, Stash y Resolución de Conflictos (Última clase)

En esta última clase se resolvieron dudas prácticas sobre situaciones reales que pasan cuando se trabaja en equipo con GitFlow y PRs.

### ¿Qué hacer cuando aprueban un PR que toca lo mismo que tú?

Esto pasa cuando alguien más estaba trabajando en los mismos archivos o líneas que tú, y su PR se mergeó a develop antes que el tuyo. Tu rama queda desactualizada y cuando intentas hacer el PR van a aparecer conflictos. Para resolverlo:

```bash
git fetch                                        # traes los cambios remotos sin aplicarlos todavía
git checkout feature/tu-rama                     # te aseguras de estar en tu rama
git merge origin/develop                         # fusionas develop actualizado en tu rama
# resuelves los conflictos manualmente en los archivos marcados
git add .
git commit -m "fix: Resuelve conflictos con develop"
git push origin feature/tu-rama                  # subes tu rama actualizada
```

### Git Stash

`git stash` guarda tus cambios temporalmente sin necesidad de hacer un commit. Es muy útil cuando necesitas cambiar de rama pero tienes cosas a medias, cuando hay conflictos que no quieres resolver en ese momento, o simplemente cuando quieres dejar el directorio limpio por un rato.

```bash
git stash                    # guarda los cambios y limpia el directorio de trabajo
git stash -m "mensaje"       # lo mismo pero con un nombre descriptivo para encontrarlo después
git stash list               # muestra todos los stashes guardados
git stash pop                # aplica el stash más reciente y lo borra de la lista
git stash apply              # aplica el stash más reciente pero lo deja guardado en la lista
```

### Git Diff

`git diff` muestra qué cambió en el código entre el estado actual y algún punto de referencia. Sirve para revisar bien qué estás a punto de commitear antes de hacerlo.

```bash
git diff                         # cambios que todavía no están en stage
git diff .                       # igual que el anterior pero sobre todo el directorio actual
git diff <archivo>               # cambios de un archivo específico que no están en stage
git diff --staged                # cambios que ya hiciste git add pero aún no commiteaste
git diff --staged <archivo>      # lo mismo pero para un archivo específico
git diff <rama1> <rama2>         # diferencias entre dos ramas
```

### Buenas prácticas al borrar una rama después del merge

Una vez que el PR fue aprobado y mergeado a develop o main, la rama ya cumplió su propósito y conviene borrarla. Esto mantiene el repositorio limpio, evita confusiones con ramas viejas y hace más fácil entender qué está en desarrollo activamente.

```bash
git branch -D <rama>             # borras la rama localmente
git push origin --delete <rama>  # borras la rama en el repositorio remoto
```

El momento correcto para hacerlo es justo después de que el PR fue mergeado exitosamente, siempre que esa rama no vaya a ser necesaria para algo más adelante.