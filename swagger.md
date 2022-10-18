# swagger

estaremos utilizando swagger para el modelado de las apis, les estaré proporcionando por el canal #swagger en el discord archivos con formato yaml seguido de los diagramas de bases de datos y el archivo sql.

cada archivo yaml representa un servicio y para poder verlo con el debido formato es necesario descargar el archivo y dirigirse a swagger editor ya sea haciendo una busqueda en internet o entrando directamente en este enlace:

https://editor.swagger.io/

una vez que esten dentro dirigirse a la barra superior y dar en la opcion file -> import file <br> para posteriormente seleccionar el archivo yaml previamente descargado para la representación del servicio.

swagger inicialmente divide la pantalla en 2 columnas, una donde se ve el contenido del archivo yaml y otra donde se representa el servicio/api con sus endpoints, esta division se puede hacer más chica o más grande, como ustedes no necesariamente necesitan modificar el yaml pueden incluso quitar la columna donde aparece el yaml.

## secciones

dentro de la representacion se encuentran las secciones que por lo regular tendremos una seccion por cada tabla en la base de datos
<img src='imagenes/seccion.png'>

la seccion cuenta con una breve descripción y los endpoints que deberá tener.

## parametros

cuando damos clic en un endpoint cuenta igualmente con una breve descripción y con una seccion de parametros:

<img src='imagenes/parametros.png'>

los parametros son datos que tienen que ser enviados ya sea por el path (url) o header, los parametros son datos que llegan a nuestro endpoint mientras no sean parte del request body.

por sierto las peticiones get y delete no pueden tener request body es por eso que los datos que recibimos por estas peticiones son unicamente por los parametros.

## request body

el request body se define debajo de los parametros, ahí mismo defino en json los datos que recibiremos en el endpoint y además ahí les explico las validaciónes que tendrán que realizar para registrar o actulizar datos en la base de datos.

<img src='imagenes/request.png'>

## responses

y por ultimo tenemos los responses, ahí aparecen los datos en formato json que tendrán que devolver y tambien los codigos http.

<img src='imagenes/responses.png'>