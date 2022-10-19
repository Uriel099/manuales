# validaciónes

Una parte fundamental de los endpoints de una api es la validación de los datos que se reciben desde el cliente para evitar que node lance excepciones a la hora de realizar una consulta a la base de datos.

hay dos maneras de validar los datos: con la librería express-validator y directamente a la base de datos, la librería de express validator nos permite hacer validaciones sencillas con los datos que recibimos del request body o header

## validaciones con express-validator 

para ver la documentación oficial haz click en el siguiente enlace: https://express-validator.github.io/docs/

A continuación les dejo ejemplos de validaciónes simples pero que pueden ser bastante utiles:

~~~js
    const { body, headers } = require('express-validator');

    //validar que un campo en el request body tenga minimo un carácter y maximo 5
    body('campo').isLength({min: 1, max: 5});
    
    //validar que un campo en el request body tenga minimo un carácter
    body('campo').isLength({min: 1});

    //validar que el id enviado en el header sea númerico
    headers('id').isNumeric()

    //validar que el campo exista
    body('campo').exists()

    //validar que el campo bandera en el request body sea booleano
    body('bandera').isBoolean()
~~~

estas validaciónes se ponen como middleware en donde se define la ruta, esto quiere decir que se tendrán que dirigir al archivo dentro de la carpeta routes del endpoint que quieran validar y poner estas validaciónes en la ruta como en el siguiente ejemplo.

~~~js
const express = require('express');
const router = express.Router();

const { body } = require("express-validator");

const {save_plan} = require('../controller/plan-controller.js')

router.post('/',
    body('ID_Carrera').isNumeric(),
    body('Clave').isLength({min: 10, max: 15}),
    body('bandera').isBoolean(),
    save_plan);

module.exports = router
~~~

En caso que los datos no cumplan con las validaciónes estos middlewares no detendrán la ejecución del programa a menos que nosotros se lo indiquemos, dentro de la función en nuestro controlador hay que obtener los errores que express-validator generá y validar si hay alguna para detener la ejecución del programa y devolver un mensaje al cliente indicandole que sus datos no son correctos

~~~js
const { validationResult } = require("express-validator");

const registra_reticula = async (req, res) => {
    const validation_errors = validationResult(req);

    if (!validation_errors.isEmpty()) {
        const response = return_error(401, 'datos con formato incorrecto');
        return res.status(401).json(response);
    }
}
~~~

## validaciónes en la base de datos

una forma de realizar validaciones en la base de datos es ejecutando una consulta de validación antes de realizar la consulta final de inserción o actualización, se pueden ejecutar consultas como las siguientes:

~~~sql
SELECT COUNT(ID_Elemento) as validacion FROM tabla WHERE ID_Elemento = 5
~~~

esta consulta contará los elementos en la tabla con ese id, en el caso que el resultado sea 0 significa que no hay un registro con ese id o si el resultado es mayor que 0 entonces si existen registros con ese id, a continuación les dejo ejemplos de como realizar estas validaciones en sus controladores:

~~~js
const pool = require('../config/mariadb.js');

const registra_reticula = async (req, res) => {
    try{
        const validacion_clave = await conn.query('SELECT count(ID_Asignatura) as result FROM Asignaturas WHERE clave = ?', [key]);
            if(parseInt(validacion_clave[0].result) > 0){
                const error = return_error(406, "La asignatura ya se encuentra registrada");
                return res.status(406).json(error);
            }

            //validar que el plan exista
            const validacion_plan = await conn.query('SELECT count(ID_PlanEstudio) as result FROM planesestudio WHERE ID_PlanEstudio = ? ', [studyPlan]);

            if(parseInt(validacion_plan[0].result) === 0){
                const error = return_error(406, "El plan de estudio no se encuentra registrado");
                return res.status(406).json(error);
            } 
    }catch(err){
        console.log(err);
        const error = return_error(500, "internal server error");
        res.status(500).json(error);
    }
}

module.exports = {registra_reticula}
~~~

en el caso que se necesite realizar algúna de estas validaciónes muchas veces tambien existe la posibilidad de convertir estas validaciones en un middleware pero esto queda a su criterio.