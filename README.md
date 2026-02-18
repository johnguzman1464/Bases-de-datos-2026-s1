 Diseño lógico de bases de datos relacionales
John Alexander Guzmán Barreto
-En base al enunciado, podemos construir un diagrama de entidad relación para exponer de mejor manera las necesidades expuestas en el enunciado.
A través del diseño lógico podemos proponer una solución al problema basándose en un modelo de datos para organizar la información (ej: tablas).
El proceso es sencillo si se posee la documentación e información necesaria:
-Cada entidad presente en el esquema conceptual representa una tabla en el esquema lógico.
-Las relaciones de muchos a muchos se modelan como una tabla nueva, esta debe contener las claves principales de ambas tablas y sus atributos correspondientes. Además, esto lleva a la creación de una llave principal propia, compuesta por las claves principales anteriores
-Las relaciones de uno a muchos se incluyen en la tabla de cardinalidad (muchos). Esto conlleva a que la tabla de “muchos”, contenga el atributo principal de la tabla con la que se relaciona.
-Se definen las Claves principales y las claves ajenas de cada tabla.
Esto nos sirve para obtener una serie de relaciones que son capaces de solucionar el problema descrito.
