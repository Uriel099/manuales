# trabajar con git

estaremos trabajando con git desde un servidor propio del tecnologico, no se utilizarán servicios como github o gitlab para el manejo del repositorio, así que contaremos con pocas herramientas gráficas para trabajar con git, de hecho este manual está orientado al uso de git utilizando git bash.
 
personalmente les recomiendo que si utilizan git bash ya que en las empresas es muy común que utilicen git con servidores propios además que puede ser más rápido trabajar así una vez que te acostumbras.

## acceso
Al utilizar nuestro propio servidor nos estaremos autenticando con ssh por lo que es necesario generar una llave utilizando git bash, si ya has generado la llave previamente no es necesario realizar los siguientes pasos.
 
generar llave ssh con git bash:
~~~
$ ssh-keygen
Generating public/private rsa key pair.
Enter file in which to save the key (/c/Users/user/.ssh/id_rsa):
~~~

por defecto genera una llave en el directorio /c/Users/user/.ssh/ con el nombre id_rsa, pueden cambiar de directorio pero les recomiendo que la dejen en esa carpeta.
 
una vez que den enter les pedirá una clave, esta la pueden dejar vacía o en caso que le pongan una clave es necesaria recordarla ya que git estará pidiendola cuando hagamos ciertas acciones en el repositorio del servidor.
 
cuando hayamos completado estos pasos entonces veremos algo similar a lo siguiente:

~~~
Your identification has been saved in id_rsa
Your public key has been saved in id_rsa.pub
The key fingerprint is:
SHA256:HSh9Qi7LNP3mzzW9Vk+fFvWAucRdbrduG9bonfzy4+c jimow@DESKTOP-AVPMJL3
The key's randomart image is:
+---[RSA 3072]----+
|        .        |
|       = .      .|
|      = * o. + o |
|     o = = .= o =|
|      o S +. . o=|
|         o  .  ==|
|          .   =+O|
|           o o+XB|
|            o *XE|
+----[SHA256]-----+
~~~

una vez que sucedió esto ya hemos generado la llave por lo que es necesario dirigirnos al directorio que especificamos e identificar la llave, en el directorio deben de aparecer dos archivos con el nombre que especificamos, uno sin extensión que es la llave privada y otro con extensión pub que es la llave pública esta es la que me tienen que proporcionar para registrar en el servidor.
 
mientras tanto creen un archivo config sin extensión en la carpeta /c/Users/user/.ssh/ y en él escriban lo siguiente:

~~~
  host developer.tecmm.mx
  user git
  identityfile ~/.ssh/id_rsa
~~~
En el identityfile hay que especificar la llave privada o el archivo sin extensión.
 
igualmente si ya cuentan con el archivo solo sería necesario que agreguen ese bloque de texto.

## Clonar el repositorio
En el siguiente repositorio está el proyecto en el que estaremos trabajando esta semana, las próximas semanas estaremos trabajando en diferentes repositorios por lo que les estaré proporcionando los diferentes comandos para clonar el repositorio, para esta semana utilizamos el siguiente comando posicionandonos en el directorio donde trabajaremos:

~~~
git clone git@developer.tecmm.mx:/opt/git/plan.git
~~~

Si definieron una clave en su llave entonces git les pedirá la clave y después de esto clonará el repositorio.
 
no olviden cambiarse al directorio del repositorio para trabajar con git

## Ramas

igualmente estaremos trabajando con ramas, en el repositorio ya existe una rama por cada uno de ustedes, si ejecutan el comando git branch -r podrán ver las ramas que ya he creado previamente.

~~~
$ git branch -r
  origin/HEAD -> origin/master
  origin/eirazoqui
  origin/erodriguez
  origin/jcortes
  origin/jnava
  origin/kgonzalez
  origin/master
  origin/nbanuelos
~~~

antes de tan siquiera comenzar a programar es necesario que se cambien a su respectiva rama, que es la que se encuentra nombrada con la primer letra de su primer nombre y seguido de su primer apellido, no creo que haya confusión en esta parte pero si es así pueden contactarme por whatsapp o discord para resolverles esta duda.

para utilizar su rama ejecutar el comando:

~~~
$   git checkout nombredesurama
~~~

igualmente tendrán que trabajar en sus endpoints asignados en clickup para no generar problemas a la hora de hacer merge a las ramas.

## repaso de git
igualmente les dejo un breve manual de como trabajar con git ya que están en su rama.

* ver los cambios que hacen falta por agregar al repositorio
~~~
$ git status
~~~

* agregar archivos con cambios al repositorio
~~~
//añadir los cambios de un archivo especificio
$ git add filename.extension
//añadir todos los cambios
$ git add .
~~~

* traer cambios de repositorio remoto
~~~
$ git pull
~~~

* hacer commit
~~~
$ git commit -m "mensaje del commit"
~~~
traer caes necesario hacer commit cada que hayan realizado un cambio así puedo rastrear el progreso que llevan.

* subir cambios al servidor
~~~
$ git push
~~~
los cambios que realicen serán de manera local por lo que es necesario que también suban esos cambios al servidor lo más pronto posible.
 
una vez que hayan terminado con sus endpoints favor de avisarme para realizar los merges, ya que no contamos con un aplicativo que nos ayude a generar los pull requests.