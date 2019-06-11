#Practica GIT. Ejercicio 1
##Alumno: Ismael Bernal - WEB VII

## RESPUESTAS PRÁCTICA
### ¿Qué comando utilizaste en el paso 11? ¿Por qué? 
**Comando:** git reset --hard HEAD~1

> Explicación: La razón de utilizar es que reset es el comando que nos permite mover el puntero HEAD, y aplicando además el modificador --hard lo que hacemos es que el cambio afecte al working copy. Además con HEAD~1 lo que hago es mover el HEAD al commit inmediatamente anterior. Es decir, retrocedo el puntero HEAD, de tal forma que ahora apunta al parent. Por lo que estamos en el punto donde TODAVÍA no habíamos modificado git-nuestro.md

### ¿Qué comando o comandos utilizaste en el paso 12? ¿Por qué? 
**Comandos:**
    Opcion a) git reset --hard HEAD@{1}
    Opcion b) --> git reflog  ...y luego --> git reset --hard 3fc1756

> Explicación: Ambas opciones son equivalentes. La primera opción lo que hace es mover el puntero HEAD al segundo resultado de git reflog. Es decir, vuelve al COMMIT que anteriormente tenía los cambios en git-nuestro.md (antes de deshacerlos en el paso 11). Otra opción sería ejecutar git reflog, y una vez vemos el listado de commits. Hacemos un git reset --hard sobre el hash que identifica el commit que tiene nuestros cambios sobre git-nuestro.md (en mi caso era el 3fc1756). Ambas opciones en este punto de la 'historia' del repositorio son equivalentes.

### El merge del paso 13, ¿Causó algún conflicto? ¿Por qué?
**Comando:** git merge master

> Explicación: este merge no dará ningún conflicto, debido a que la rama styled no tiene nada que mergear desde master. Ya que, la rama master es parent de styled, y styled actualizada en cuanto a su parent (lo que no quiere decir que sean iguales en contenido). Es decir, desde que se creo la rama style desde master. Master no ha tenido ningún cambio. Por tanto no hay nada que mergear.

### El merge del paso 19, ¿Causó algún conflicto? ¿Por qué?
**Comandos:**
    1) Cambio a la rama styled (que es la que absorve a htmlify): git checkout styled
    2) Inicio el merge: git merge htmlify
    3) En este punto se generan los conflictos. Se resuelven sobre el fichero git-nuestro.md (ver punto 20)

> Explicación: si que se generaron conflictos. Esto es debido a que tanto styled como htmlify hacían modificaciones en las mismas lineas de git-nuestro.md. Por esta razón git nos solicita que resolvamos estos conflictos

### El merge del paso 21, ¿Causó algún conflicto? ¿Por qué?
**Comandos:**
    1) Primero nos posicionamos en master: git checkout master
    2) Después hacemos el merge: git merge styled

> Explicación: en este caso no se generaron conflictos. Porque el fichero git-nuestro.md no tenía modificaciones posteriores a las que "vienen" de la rama styled. Como Styles se creo originalmente desde master, Git no tiene ningún problema a la hora de mergear en master la nueva versión de git-nuestro.md que viene de styled.

### ¿Qué comando o comandos utilizaste en el paso 25? 
**Comando:** git log --graph --decorate --pretty=oneline

### El merge del paso 26, ¿Podría ser fast forward? ¿Por qué?
**Comando:** git merge title

> Explicación: Si. Este merge también podríamos realizarlo en modo default (fast-forward), dado que el commit en el que nos encontramos en MASTER es un parent del de la rama que queremos mergear. Es decir, ambas ramas forman una lista. 

### ¿Qué comando o comandos utilizaste en el paso 27?
**Comando:** git reset HEAD~1  (es suficiente con volver al commit anterior para deshacerlo)

### ¿Qué comando o comandos utilizaste en el paso 28?
**Comando:** git checkout -- git-nuestro.md

### ¿Qué comando o comandos utilizaste en el paso 29? 
**Comando:** git branch -D title   (estamos en master actualmente. Por lo que podemos borrar title)

### ¿Qué comando o comandos utilizaste en el paso 30?
**Comandos:** 
    1) git reset --hard HEAD@{1}   (vuelvo al commit indicado por git reflog en segunda posición)
    2) O bien, git reflog, buscar el commit donde hicimos el merge --no-ff y hacer git reset --hard sobre ese hash

### ¿Qué comando o comandos usaste en el paso 32?
**Comandos:** 
    1) git reflog
    2) git reset --hard af4405f  (este es el hash del primer commit en mi caso)

### ¿Qué comando o comandos usaste en el punto 33?
**Comandos:** 
    1) git reflog
    2) git reset --hard e5619b0  (este es el hash del último commit en mi caso)


-----
## RESTO DEL EJERCICIO COMPLETO
-----


### 1) Crear un repositorio
**Comando:** git init

### 2) Crear un archivo git-nuestro.md con el contenido:
    Git nuestro
    Git nuestro que estas en los repos
    Comprimidos sean tus commitsVenga a nosotros tu log
    En el local como en el remote
    Danos hoy nuestro pull de cada día
    Perdona nuestros conflictos
    Como también perdonamos los de otros geeks
    No nos dejes caer en detached HEAD
    y líbranos de SVN
    git commit --amend

**Comando:** nano git-nuestro.md

### 3) Añadir git-nuestro.md al staging area
**Comando:** git add git-nuestro.md

### 4) Mover lo que hay en el staging area al repositorio
**Comando:** git commit -m "Primer commit sobre git-nuestro.md"

### 5) Crear una rama llamada “styled”
**Comando:** git branch styled

### 6) Listar las ramas que hay en el repositorio
**Comando:** git branch

### 7) Moverse a la rama “styled”
**Comando:** git checkout styled

### 8) Comprobar que se está en la rama correcta
**Comando:** git branch

### 9) Modificar en el archivo git-nuestro.md:
    *Git* nuestro que estas en los repos
    Comprimidos sean tus *commits*
    Venga a nosotros tu *log*
    En el local como en el *remote*
    Danos hoy nuestro *pull* de cada día
    Perdona nuestros *conflictos*
    Como también perdonamos los de otros geeks
    No nos dejes caer en *detached HEAD*
    y líbranos de *SVN*
    `git commit --amend`

**Comando:** nano git-nuestro.md

### 10)Añadir los cambios al staging área y luego pasarlos al repositorio
**Comandos:** 
    git add git-nuestro.md
    git commit -m "Modificando git-nuestro con estilos markdown"

### 11) Deshacer el último commit (perdiendo los cambios realizados en el working copy)
**Comando:** git reset --hard HEAD~1

### 12) Rehacer el último commit (el que acabamos de deshacer)
**Comandos:**
    Opcion a) git reset --hard HEAD@{1}
    Opcion b) --> git reflog  ...y luego --> git reset --hard 3fc1756

### 13) Hacer un merge con ‘master’ (styled absorbe a master)
**Comando:** git merge master

### 14) Volver a la rama master
**Comando:** git checkout master

### 15) Crear una nueva rama llamada “htmlify”
**Comando:** git branch htmlify

### 16) Cambiar a la rama htmlify
**Comando:** git checkout htmlify

### 17) Modificar en el archivo git-nuestro.md:
    <p><em>Git</em> nuestro que estas en los repos<br />
    Comprimidos sean tus <em>commits</em><br />
    Venga a nosotros tu <em>log</em><br />
    En el local como en el <em>remote</em><br />
    Danos hoy nuestro <em>pull</em> de cada día<br />
    Perdona nuestros <em>conflictos</em><br />
    Como también perdonamos los de otros geeks<br />
    No nos dejes caer en <em>detached HEAD</em><br />
    y líbranos de <em>SVN</em><br />
    <code>git commit --amend</code></p>

**Comando:** git nano git-nuestro.md

### 18) Hacer un commit
**Comando:** git commit -m "Dando estilos html al git-nuestro"

### 19) Hacer un merge de “htmlify” en “styled” (styled absorbe a htmlify)
**Comandos:**
    1) Cambio a la rama styled (que es la que absorve a htmlify): git checkout styled
    2) Inicio el merge: git merge htmlify
    3) En este punto se generan los conflictos. Se resuelven sobre el fichero git-nuestro.md (ver punto 20)

### 20) Si hay conflictos, deberemos resolverlos quedándonos con el contenido de la rama “styled”.
**Comandos:**
    1) Para resolverlos: nano git-nuestro.md
    2) Una vez resueltos (quedandonos con las modificaciones de la rama styled): git add git-nuestro.md
    3) Por último commit: git commit -m "Merge de htmlify en styled

### 21) Desde “master”, hacer un merge con “styled”
**Comandos:**
    1) Primero nos posicionamos en master: git checkout master
    2) Después hacemos el merge: git merge styled

### 22) Crear una rama “title” y cambiarse a esa rama
**Comandos:**
    1) git branch title
    2) git checkout title

### 23) Añadir un título (a tu gusto) al archivo git-nuestro.md y hacer un commit. 
**Comandos:**
    1) nano git-nuestro.md
    2) git add git-nuestro.md
    3) git commit -m "Añadiendo titulo al fichero de la rama title"

### 24) Volver a la rama master
**Comando:** git checkout master

### 25) Dibujar el diagrama
**Comando:** git log --graph --decorate --pretty=oneline

### 26) Hacer un merge “no fast-forward” de “title” en “master” (master absorbe a title)
**Comando:** git merge --no-ff title

### 27) Deshacer el merge (sin perder los cambios del working copy)
**Comando:** git reset HEAD~1

### 28) Descartar los cambios
**Comando:** git checkout -- git-nuestro.md

### 29) Eliminar la rama “title”
**Comando:** git branch -D title 

### 30) Rehacer el merge que hemos deshecho
**Comandos:** 
    1) git reset --hard HEAD@{1}
    2) O bien, git reflog, buscar el commit donde hicimos el merge --no-ff y hacer git reset --hard sobre ese hash

### 31) Volver a master y eliminar el resto de ramas
**Comandos:** 
    1) git checkout master
    2) git branch -D styled
    3) git branch -D htmlify
    4) git push origin --delete styled
    5) git push origin --delete htmlify

### 32) Volver al commit inicial cuando se creó el poema
**Comandos:** 
    1) git reflog
    2) git reset --hard af4405f  (este es el hash del primer commit en mi caso)


### 33) Volver al estado final, cuando pusimos título al poema
**Comandos:** 
    1) git reflog
    2) git reset --hard e5619b0  (este es el hash del último commit en mi caso)


### 34) Crear los siguientes tags:  inicial: en el primer commit styled: modificación del paso 10  htmlify: modificación del paso 17-18   title: modificación del paso 30
**Comandos:** 
    1) git reflog
    2) git reset af4405f
    3) git tag initial
    4) git reset 50a849e
    5) git tag styled
    6) git reset 63e1fa6
    7) git tag htmlify
    8) git reset e5619b0
    9) git tag title
    10) git push origin --tags


### 35) Ir al tag htmlify
**Comandos:** 
    1) git reset htmlify
