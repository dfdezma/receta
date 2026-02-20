# Ejercicios básicos con Git

## 1- En caso de no haberlo hecho antes, configura tus datos de identificación para todos los repositorios git de tu usuario en los laboratorios.
git config --global user.email "d.fernandezma.2023@alumnos.urjc.es"

git config --global user.name "dfdezma"

## 2- En caso de no haberlo hecho antes, configura tus datos de identificación para todos los repositorios git de tu usuario en los laboratorios.

git config --list

## 3- Crea un directorio denominado receta e inicializa un repositorio de git dentro del mismo mediante el comando apropiado.

git init -b main .

## 4- Verifica su correcta creación a través del comando git status y analiza la información que devuelve éste.

git status

SALIDA:
En la rama main

No hay commits todavía

no hay nada para confirmar (crea/copia archivos y usa "git add" para hacerles seguimiento)

## 5a-  A continuación, crea dentro dos ficheros dentro del directorio.

echo "#Instrucciones.txt
Trocea el aguacate
Trocea la cebolla
Exprime la lima
Añade sal
Mezcla los ingredientes" > Instrucciones.txt

echo "#Ingredientes.txt
2 aguacates
2 limas
2 cucharaditas de sal" > Ingredientes.txt

## 5b- Y vuelve a verificar con git status el estado del repositorio. ¿Qué información devuelve este comando? ¿En qué cambia con respecto a su anterior ejecución?

git status

SALIDA:
En la rama main

No hay commits todavía

Archivos sin seguimiento:
 (usa "git add <archivo>..." para incluirlo a lo que será confirmado)
Ingredientes.txt
Instrucciones.txt

no hay nada agregado al commit pero hay archivos sin seguimiento presentes (usa "git add" para hacerles seguimiento)

En la salida vemos que nos dice que tenemos dos ficheros untracked (Ingredientes.txt e Instrucciones.txt) ya que no los hemos añadido al staging area
En la anterior salida nos salía que no había archivos untracked ni nada en el repositorio

## 6- Añade los ficheros creados al staging area (ficheros cuyos cambios serán registrados en el próximo commit), usando el comando git add, y vuelve a verificar el estado del repositorio

git add Instrucciones.txt Ingredientes.txt
git status

SALIDA:
En la rama main

No hay commits todavía

Cambios a ser confirmados:
 (usa "git rm --cached <archivo>..." para sacar del área de stage)
nuevos archivos: Ingredientes.txt
nuevos archivos: Instrucciones.txt

Ya no sale que no hayan archivos untracked, sino que faltan cambios por ser confirmados

## 7-  Registra los cambios que se han producido en el repositorio, añadiendo al mismo la siguiente descripción: ”Añadimos las instrucciones e ingredientes de la receta”. Utiliza para ello el comando commit -m <description>.

git commit -m "Añadimos las instrucciones e ingredientes de la receta"

## 8-  Registra los cambios que se han producido en el repositorio, añadiendo al mismo la siguiente descripción: ”Añadimos las instrucciones e ingredientes de la receta”. Utiliza para ello el comando commit -m <description>.

UTILIDAD -m:
-m <msg>, --message=<msg>
           Use the given <msg> as the commit message. If multiple -m options
           are given, their values are concatenated as separate paragraphs.

           The -m option is mutually exclusive with -c, -C, and -F.

## 9- Añade 1/2 cebolla a la lista de ingredientes y la instrucción Disfrútalo! a la de instrucciones. Utiliza el comando necesario para visualizar en que han cambiado exactamente los ficheros del repositorio.

echo "1/2 cebolla" >> Ingredientes.txt 
echo 'Disfrútalo!' >> Instrucciones.txt

git diff

SALIDA:
diff --git a/Ingredientes.txt b/Ingredientes.txt
index 0e9d1d4..8b60850 100644
--- a/Ingredientes.txt
+++ b/Ingredientes.txt
@@ -2,3 +2,4 @@
 2 aguacates
 2 limas
 2 cucharaditas de sal
+1/2 cebolla
diff --git a/Instrucciones.txt b/Instrucciones.txt
index 24acdec..c9c9a91 100644
--- a/Instrucciones.txt
+++ b/Instrucciones.txt
@@ -4,3 +4,4 @@ Trocea la cebolla
 Exprime la lima
 Añade sal
 Mezcla los ingredientes
+Disfrútalo!

Vemos las diferencias en ambos ficheros, indicándonos con un + las nuevas líneas añadidas

## 10a- Añade ambos al staging area y registra individualmente cada uno de estos cambios de la siguiente manera:

git add Ingredientes.txt
git commit -m "añade 1/2 cebolla"
git add Instrucciones.txt
git commit
git log
git status

## 10b- ¿Que efecto tiene no utilizar el flag -m al hacer commit?

Por defecto no permite hacer un commit sin mensaje, y al ejecutar el comando de git commit sin más, te llevará a un editor de texto para que escribas un mensaje. Si no escribes nada, abortará el commit.

## 11- Ejecuta el comando git log. ¿Qué información devuelve éste? ¿En que se diferencia de git status? ¿Que nos indica si lo usamos con el flag –stat?

git log

Este comando devuelve información de todos los commits del repositorio y a cuál de ellos apunta cada rama local, remota... También nos dice el commit hash de cada commit, útil para usar otros comandos, mostrar commits...

git status

Este comando nos da información del estado en las diferentes zonas del repositorio (directorio local, staging area y commits). Es útil para ver si todo está sincronizado o no

git log --stat

Da información de los commits como git log, pero con información más detallada de cada commit, poniendo las modificaciones hechas en cada uno de estos.

## 12- Revisa el contenido de un commit concreto (en este caso, el ultimo realizado) a través de su identificador hash mediante el comando git show <hash1>.

git show fc626c280de6483d8b95d2fa9bbab0cd2530d1e8

Con este comando podemos ver información del commit y más detalladamente los cambios que se hicieron, qué se insertó o eliminó...

SALIDA:
commit fc626c280de6483d8b95d2fa9bbab0cd2530d1e8 (HEAD -> main)
Author: dfdezma <d.fernandezma.2023@alumnos.urjc.es>
Date:   Fri Feb 20 20:22:56 2026 +0100

    Disfrutar

diff --git a/Instrucciones.txt b/Instrucciones.txt
index 24acdec..c9c9a91 100644
--- a/Instrucciones.txt
+++ b/Instrucciones.txt
@@ -4,3 +4,4 @@ Trocea la cebolla
 Exprime la lima
 Añade sal
 Mezcla los ingredientes
+Disfrútalo!


## 13- Visualiza las diferencias entre los dos últimos commits a través de sus respectivos hashes utilizando para ello el comando git diff <hash1> <hash2>.

git diff fc626c280de6483d8b95d2fa9bbab0cd2530d1e8 9647c5b34b3d5b4876353c60f2b8d17d43677862

SALIDA: 
diff --git a/Instrucciones.txt b/Instrucciones.txt
index c9c9a91..24acdec 100644
--- a/Instrucciones.txt
+++ b/Instrucciones.txt
@@ -4,4 +4,3 @@ Trocea la cebolla
 Exprime la lima
 Añade sal
 Mezcla los ingredientes
-Disfrútalo!

Vemos que la salida nos indica la línea de "Disfrútalo!" que añadimos en el último commit
