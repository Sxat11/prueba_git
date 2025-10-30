# Práctica guiada Git

Creamos un nevo directorio prueba_git y accedemos a él

```bash
usuario@DESKTOP-JHGTBRI MINGW64 ~
$ mkdir prueba_git

usuario@DESKTOP-JHGTBRI MINGW64 ~
$ cd prueba_git
```

Crearemos mediante un editor de texto dos archivos dentro de prueba_git: texto.txt y script.sh

```bash
usuario@DESKTOP-JHGTBRI MINGW64 ~/prueba_git
$ nano texto.txt

usuario@DESKTOP-JHGTBRI MINGW64 ~/prueba_git
$ nano script.sh
```

En texto.txt escribiremos 3 números(uno,dos,tres) y en script.sh añadiremos estas 2 líneas:

```bash
 echo Listado completo
 ls -l
```

## 1.Introducción

Añadiremos nuestro directorio prueba_git como nuevo repositorio local.

```bash
usuario@DESKTOP-JHGTBRI MINGW64 ~/prueba_git
$ git init
Initialized empty Git repository in C:/Users/usuario/prueba_git/.git/
```

Esto creará un direcctorio denominado .git en el que se guardará toda la información de histórico del repositorio.

Por cada versión de cada elemento que
haya en el repositorio, aquí se hará una copia con una estructura determinada.

Para poder verlo podemos usar "$ git status"

```bash
usuario@DESKTOP-JHGTBRI MINGW64 ~/prueba_git (main)
$ git status
On branch main

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        script.sh
        texto.txt

nothing added to commit but untracked files present (use "git add" to track)
```

Este mensaje significa que aunque estos archivos estén en el directorio, no están
gestionados por git. ¡Los no gestionados no se
replicarán en otras máquinas con las que estemos compartiendo!

$ git branch -m main --> Nos permite cambiar el nombre de la rama main o master (yo la tengo por defecto en main).

```bash
usuario@DESKTOP-JHGTBRI MINGW64 ~/prueba_git (main)
$ git branch -m master

usuario@DESKTOP-JHGTBRI MINGW64 ~/prueba_git (master)
$ git branch -m main
```

## 2. Añadiendo archivos

$ git add -> Nos permite añadir archivos a rastreado.

```bash
usuario@DESKTOP-JHGTBRI MINGW64 ~/prueba_git (main)
$ git add script.sh
warning: in the working copy of 'script.sh', LF will be replaced by CRLF the next time Git touches it

usuario@DESKTOP-JHGTBRI MINGW64 ~/prueba_git (main)
$ git status
On branch main

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   script.sh

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        texto.txt
```

Utilizando $git status podemos observar que texto.txt sigue sin estar rastreado pero script.sh pasa a ser un
archivo rastreado por git (tracked).

Esto significa que git comprobará si hay cambios desde la última versión. Si
embargo aún no está confirmado. Esto es, no se sincronizará con los equipos
remotos.

$ git commit -> para establecer una versión
sincronizada del archivo. 
```bash
usuario@DESKTOP-JHGTBRI MINGW64 ~/prueba_git (main)
$ git commit -m "Confirmación inicial"
[main (root-commit) 5df1c20] Confirmación inicial
 1 file changed, 2 insertions(+)
 create mode 100644 script.sh

usuario@DESKTOP-JHGTBRI MINGW64 ~/prueba_git (main)
$ git status
On branch main
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        texto.txt

nothing added to commit but untracked files present (use "git add" to track)
```
//git cat-file

Añadimos también texto.txt:

```bash
usuario@DESKTOP-JHGTBRI MINGW64 ~/prueba_git (main)
$ git add texto.txt
warning: in the working copy of 'texto.txt', LF will be replaced by CRLF the next time Git touches it

usuario@DESKTOP-JHGTBRI MINGW64 ~/prueba_git (main)
$ git commit -m "Añadiendo archivo texto.txt"
[main 48c284d] Añadiendo archivo texto.txt
 1 file changed, 3 insertions(+)
 create mode 100644 texto.txt

usuario@DESKTOP-JHGTBRI MINGW64 ~/prueba_git (main)
$ git status
On branch main
nothing to commit, working tree clean
```

## 3. Modificando archivos

Le añadiremos un nuevo número a texto.txt.

Git lo toma como “modificado”, pero indica que no hay cambios
agregados al commit. 

```bash
usuario@DESKTOP-JHGTBRI MINGW64 ~/prueba_git (main)
$ nano texto.txt

usuario@DESKTOP-JHGTBRI MINGW64 ~/prueba_git (main)
$ git status
On branch main
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   texto.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

Para prepararlo para el siguiente commit hay que ejecutar de nuevo add. Add
es un comando que además de añadir a rastreo nuevos archivos, los prepara para
el siguiente commit

```bash
usuario@DESKTOP-JHGTBRI MINGW64 ~/prueba_git (main)
$ git add texto.txt
warning: in the working copy of 'texto.txt', LF will be replaced by CRLF the next time Git touches it

usuario@DESKTOP-JHGTBRI MINGW64 ~/prueba_git (main)
$ git status
On branch main
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   texto.txt
```
Si se hace ahora el commit, confirmaría la versión anterior (la que aparece en
verde), no la última modificación. Lo que implicaría que al sincronizarlo en otro
equipo (aun no hemos visto como se hace) sincronizaría dicha versión (la verde).//
``` bash
usuario@DESKTOP-JHGTBRI MINGW64 ~/prueba_git (main)
$ git add texto.txt
warning: in the working copy of 'texto.txt', LF will be replaced by CRLF the next time Git touches it

usuario@DESKTOP-JHGTBRI MINGW64 ~/prueba_git (main)
$ git commit -m "Ampliada la explicación del texto"
[main 2e4f462] Ampliada la explicación del texto
 1 file changed, 2 insertions(+)

usuario@DESKTOP-JHGTBRI MINGW64 ~/prueba_git (main)
$ git status
On branch main
nothing to commit, working tree clean
```
Vuelve a estar todo limpio.

## 4. Información (git show y git log)
Si continuamente necesito pasar de
modificados a la de preparación mediante add y luego confirmar mediante commit,
puedo saltarme un paso ejecutando el comando: $ git commit -a -m “Nueva versión”

```bash
usuario@DESKTOP-JHGTBRI MINGW64 ~/prueba_git (main)
$ git commit -a -m "Nueva versión"
On branch main
nothing to commit, working tree clean
```
$ git show -> Permite ver información sobre la última versión confirmada
```bash
usuario@DESKTOP-JHGTBRI MINGW64 ~/prueba_git (main)
$ git show
commit 2e4f462861b5f705dcfc57d13c8765b29999c7ed (HEAD -> main)
Author: Yusuf Dikeç <manusaxoalto@gmail.com>
Date:   Thu Oct 30 00:42:15 2025 +0100

    Ampliada la explicación del texto

diff --git a/texto.txt b/texto.txt
index cda1a21..11ce7ce 100644
--- a/texto.txt
+++ b/texto.txt
@@ -1,3 +1,5 @@
 uno
 dos
 tres
+cuatro
+cinco
```
$ git log -> Sale más información
```bash
usuario@DESKTOP-JHGTBRI MINGW64 ~/prueba_git (main)
$ git log
commit 2e4f462861b5f705dcfc57d13c8765b29999c7ed (HEAD -> main)
Author: Yusuf Dikeç <manusaxoalto@gmail.com>
Date:   Thu Oct 30 00:42:15 2025 +0100

    Ampliada la explicación del texto

commit 48c284d755f9bca17d7e485a6de924bf069a0207
Author: Yusuf Dikeç <manusaxoalto@gmail.com>
Date:   Thu Oct 30 00:38:55 2025 +0100

    Añadiendo archivo texto.txt

commit 5df1c200645df2a4e6712e4808c04c6d7b8cc913
Author: Yusuf Dikeç <manusaxoalto@gmail.com>
Date:   Thu Oct 30 00:34:19 2025 +0100

    Confirmación inicial
```

## 5. Diferencias (git diff)
Le añadimos una línea 6 y eliminamos otra.
```bash
usuario@DESKTOP-JHGTBRI MINGW64 ~/prueba_git (main)
$ nano texto.txt
```

$ git diff --> p  ara conocer las diferencias entre un archivo modificado y el que se ha confirmado en la última versión
```bash
usuario@DESKTOP-JHGTBRI MINGW64 ~/prueba_git (main)
$ git diff
warning: in the working copy of 'texto.txt', LF will be replaced by CRLF the next time Git touches it
diff --git a/texto.txt b/texto.txt
index 11ce7ce..b9c60b3 100644
--- a/texto.txt
+++ b/texto.txt
@@ -1,5 +1,5 @@
 uno
 dos
-tres
 cuatro
 cinco
+seis
```
Después ejecutamos : $ git commit -a -m "Probando diff"
```bash
usuario@DESKTOP-JHGTBRI MINGW64 ~/prueba_git (main)
$ git commit -a -m "Probando diff"
warning: in the working copy of 'texto.txt', LF will be replaced by CRLF the next time Git touches it
[main 51581ea] Probando diff
 1 file changed, 1 insertion(+), 1 deletion(-)
```
Ahora añadimos la línea (siete), luego ejecutamos de nuevo -git diff.

```bash
usuario@DESKTOP-JHGTBRI MINGW64 ~/prueba_git (main)
$ nano texto.txt

usuario@DESKTOP-JHGTBRI MINGW64 ~/prueba_git (main)
$ git diff
warning: in the working copy of 'texto.txt', LF will be replaced by CRLF the next time Git touches it
diff --git a/texto.txt b/texto.txt
index b9c60b3..5d9f7a2 100644
--- a/texto.txt
+++ b/texto.txt
@@ -3,3 +3,4 @@ dos
 cuatro
 cinco
 seis
+siete
```

## 6. Ignorar archivos (.gitignore)
Cuando empiezo a tener una cantidad de archivos importantes suele suceder que hay algunos que no me interesa gestionar a nivel de versiones.


Añadadiremos a nuestro directorio el archivo Hola.java

## 7. Tags y gestión de versiones (git tag y git checkout)
El número identificativo de la versión es un código único que aparece al lado de la palabra commit de cada versión. El nuestro es:

El resultado es información sobre el commit y la comparación de dicha versión con
la previa.

$ git tag v0.7 --> añade un tag y si queremos añadir la versión actual simplemente v.X.X. 

$ git tag v0.3 b34f694ad7dd653ea8c05c2645a045e4a444c06e

$ git log --oneline --> Es una forma resumida (en una línea) de escribir el log

$ git checkout v0.3 --> para acceder a una versión antigua para revisar algo.

$ git checkout main --> para acceder a la versión más reciente.

Los tags se almacenan en el directorio .git/refs/tags


## 8. Ramas
Una gran utilidad de los sistemas de control de versiones es la realización de
ramas, es decir, archivos paralelos a los principales con el objetivo de hacer
pruebas o poner en práctica ideas. 

$ git branch --> Nos permite crear una rama 

Tras el log aparecen dos ramas, la principal
masin, y la que has creado (Prueba).

Ahora si sigues cambiando cosas y haces commits lo haces en master, porque es
donde apunta HEAD que es el puntero de trabajo. 

git branch

Sale el listado de ramas y marcada con asterisco la rama en la que te encuentras
trabajando (coincide con la del prompt).

$ git switch --> Nos permite cambiar de rama

$ git merge --> junta la rama secundaria con la principal

Esto en ocasiones informa de conflictos o posiblesproblemas.


## 9. Eliminar y quitar de seguimiento

$ git rm --> Elimina archivos
$ git reset HEAD *.class

## 10. Repositorios remotos: GitHub

