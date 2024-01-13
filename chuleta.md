## Conceptos mínimos que tenemos que saber sobre el control de versiones

**Control de versiones** es un sistema que permite gestionar y controlar los cambios realizados en el código fuente u otros tipos de archivos a lo largo del tiempo. Este sistema ayuda a rastrear las modificaciones, facilita la colaboración entre desarrolladores y permite revertir a versiones anteriores en caso de problemas. También es útil para mantener un historial detallado de las actualizaciones, facilitando la identificación de errores y la implementación de nuevas características.

**Repositorio Local:** Es una copia del repositorio en tu máquina local. Permite realizar cambios, commits y experimentar sin afectar el repositorio remoto.

**Copia Local:** Es simplemente la versión del proyecto que tienes almacenada en tu máquina. Esta copia puede ser una réplica del repositorio remoto o una rama específica que hayas clonado o descargado.

**Stage:** Es un área intermedia entre tu copia local y el repositorio local. Aquí colocas los archivos que deseas incluir en tu próximo commit. Permite revisar y organizar los cambios antes de comprometerlos al historial del repositorio.

**Repositorio Remoto:** Es un repositorio alojado en un servidor externo o en la nube. Permite compartir y sincronizar cambios entre diferentes copias locales.

**Log:** Es un registro que muestra el historial de commits en un repositorio. Proporciona información sobre quién realizó un cambio, cuándo y qué cambios se realizaron.

**Conflicto:** Ocurre cuando se modifica el mismo archivo y las mismas lineas en dos cambios distintos, git no sabe cual de las dos versiones almacenar. Tienen que ser solucionados a mano eligiendo entre las dos caras del propio conflicto en cada una de las partes del documento en las que se hayan modificado las mismas líneas.

### Estados de un fichero:

- **Sin Seguimiento:** El archivo no está siendo rastreado por Git.
- **Confirmado:** Los cambios del archivo han sido registrados en un commit.
- **Modificado:** El archivo ha sido modificado desde el último commit.
- **Preparado:** Los cambios del archivo han sido seleccionados para ser incluidos en el próximo commit.
- **Ignorado:** Git está configurado para ignorar este archivo y no rastrear sus cambios.

### Operaciones:

**COMMIT:** Confirmar los ficheros preparados para su almacenamiento en el repositorio.

**ADD:** Realiza una copia de un fichero modificado, poniéndola en la zona de preparación para poder ser confirmada.

**CLONE:** Replica un repositorio entero con todo su historial de cambios y actualiza el directorio local

**PUSH:** Es la operación en la que se envían al repositorio centralizado un commit o conjunto de commits, incluido una rama entera.

**PULL:** Es la operación en la que se actualiza el repositorio local y el directorio local con commits que provienen del repositorio remoto.

**FETCH:** Trae los commits de un repositorio remoto a un repositorio local, pero no actualiza el directorio local. Se utiliza menos que las otras.

**MERGE:** Crea un commit en el que se guardan los cambios de la rama

**REBASE** : Transplanta todo lo hecho en la direccion que se le diga "git rebase main"

**FORK:** Clone que se hace dentro del mismo servidor. Por ejemplo, el repositorio original y el clonado ambos residen en GitHub, GitLab, o Bitbucket, etc. Al original se le suele llamar

**PULL REQUEST (entre repositorios):** Petición que hace el desarrollador de que los cambios hechos en su repositorio clonado mediante un FORK sean incorporados al repositorio original. Permite hacer una revisión del código antes de hacer el merge correspondiente. El MERGE se HACE EN el REPO remoto.

**Servicios de repositorio remoto:** GitHub, GitLab, BitBucket, etc.

**Clientes gráficos para el control de versiones:** gitg, gitkraken, gitblade, etc.

## En el intérprete de comandos de git-bash

- **Mostrar en qué directorio estamos:** pwd
- **Crear un directorio:** mkdir \<dir\>
- **Cambiar de directorio:** cd \<dir\>
- **Mostrar la lista de ficheros de un directorio:** ls [-l] [-a]
- **Borrar un fichero:** rm \<file\>
- **Cambiar (mover) un fichero de directorio:** mv \<source\> \<dest\>

## En Local

- **Crear repositorio:** git init
- **Ignorar fichero:** incluir un .gitignore
- **Preparar para ser confirmados:** git add

git add --all añade todos los archivos con cambios

- **Confirmar cambios en local:** git commit -m \<mensaje\>
- **Muestra los cambios de un archivo con el que hay en el repositorio** : git diff \<file\>
- **Deshacer la operación de preparar:** git reset \<nombre del archivo\>
- **Deshacer la operación de confirmar en sus tres niveles (soft, mixed y hard):**

Si hacemos un git reset - -soft \<nombre commit\> lo que conseguimos es eliminar el último commit y hacer que los cambios vuelvan al stage, con el - -mixed conseguimos que los cambios de este commit vuelvan a nuestro working directory y con el - -hard conseguimos volver directamente al commit anterior, perdemos todo lo que contenía ese commit.

- **Identificar el estado de ficheros en repo local:** git status
- **Descartar cambios cambiando de commit:** Para cambiar de commit y que se pierdan todos los cambios que no han sido confirmados tenemos que hacer un git checkout \<nombre del commit\>.
- **Crear una rama:** git branch \<nombre rama\>.

git branch -d \<nombre rama\> borra la rama

- **Cambiar de rama:** git checkout \<nombre rama\> / git switch \<nombre rama\>
- **Fundir los cambios de una rama en otra:**

Para fundir cambios se hace primero un git checkout \<rama principal\> y luego git merge \<rama a fundir\> , con esta opción conseguimos que el commit más reciente de la rama que queremos fusionar se imponga en la rama con la que la queremos fusionar creando un commit adicional con la misma información que el más reciente de la otra rama pero con un mensaje donde se dirá que ese commit se creó debido a fusionar cierta rama con otra.

- **Injertar una rama en otra** :

Para injertar se hace primero un git checkout \<rama a injertar\> y luego git rebase \<rama principal\>, con este comando lo que se consigue es trasplantar todos los commit de la rama en otra que se pasa como parámetro.

## En remoto (con GitHub)

- **Configurar git para que trabaje tras un proxy:**

git config --global http.proxy http://\<nombre de usuario\>:\<password\>@\<direccion\_ip\>:\<puerto\>

Siendo 'nombre de usuario' el nombre de usuario para autentificarse en el servidor proxy, 'password' la contraseña para identificarse en el servidor proxy, 'direccion\_ip' la dirección del servidor de proxy y 'puerto' en el que está escuchando el proxy.

Si queremos deshabilitar el uso del proxy usamos:

git config --global --unset http.proxy

- **Replicar un repositorio remoto localmente en nuestra máquina:** git clone \<url repo\>
- **Replicar un repositorio local en un servidor remoto:**

git remote add origin \<url repo\>

Tras esto nos quedaría crear una nueva rama (git branch main), añadir los archivos deseados (git add), realizar el commit (git commit -m \<mensaje\>) y hacer el push (git push -u origin main).

- **Traer los cambios de un repositorio remoto a un repositorio local:**

git pull

Descarga los archivos actualizados del repositorio remoto y realiza un merge entre el repositorio local y el remoto.

git fetch \<remote\> solo trae datos a tu repositorio local ni lo combina con tu trabajo ni modifica el trabajo que llevas hecho.

- **Resolver los conflictos que se puedan producir al traerse estos cambios:** Buscando \<\<\<\<\<\<\<, ======= y \>\>\>\>\>\>\> y editando el archivo manualmente con los cambios deseados.

- **Enviar los cambios de un repositorio local a uno remoto:** git push \<rama remota\> \<rama local\>
- **Enviar una rama local al repositorio remoto de manera que la local quede enganchada (haga tracking de) la remota:** git push -u \<rama remota\> \<rama local\>
- **Incorporar a ramas locales cambios que se producen en el repositorio remoto:** git pull \<rama remota\> \<rama local\>
- **Crear un repositorio remoto vacío:**

git init

git remote add origin \<url repo\>

git push -u origin \<rama local\>

- **Invitar a colaboradores.**

1. En el repositorio en github, haz clic en Configuración.
2. En la sección "Acceso" de la barra lateral, haz clic en Colaboradores.
3. Haz clic en Agregar personas, escribe el nombre del colaborador y haga clic en Agregar NOMBRE al REPOSITORIO.
4. El usuario recibirá un correo electrónico invitándolo al repositorio. Una vez que acepte la invitación, tendrá acceso de colaborador a tu repositorio.

- **Realizar un pull request entre dos ramas de un repositorio remoto.**

Ahora al ir a la página del repositorio en GitHub, en el menú de ramas "Branch" hacer clic en una rama que no sea la principal.

Al clicar la rama podremos darle al botón 'Compare / pull-request', el cual permite hacer el pull a la rama inicial. Podemos hacer una descripción de qué vamos a subir y, cuando terminemos, pulsamos en 'Create pull request'.

- **Realizar un pull request entre dos repositorios que resultaron de un Fork.**

Ve a tu repositorio en GitHub y verás un botón llamado "Pull request", haz clic en él. Podemos hacer una descripción de qué vamos a subir y, cuando terminemos, pulsamos en 'Create pull request'.
