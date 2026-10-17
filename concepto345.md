## **APLICACIÓN DE LA NORMALIZACIÓN EN EL DISEÑO LÓGICO**

La normalización permite organizar la información de la base de datos para reducir la duplicación de datos, mantener la integridad de la información y evitar anomalías al insertar, actualizar o eliminar registros. Para el sistema de gestión de alquiler de cuartos, se aplican las tres primeras formas normales.

---

### **1. PRIMERA FORMA NORMAL (1FN)**

La primera forma normal establece que cada campo debe contener un único valor y que no deben existir grupos de datos repetidos dentro de una misma tabla.

En el sistema de alquiler de cuartos, los datos de los inquilinos se almacenan de manera individual. Por ejemplo, el nombre, apellido, carnet de identidad, teléfono, correo electrónico y dirección se registran en sus respectivos campos.

Asimismo, los servicios adicionales, como internet, electrodomésticos y parqueo, se almacenan en una tabla independiente denominada `servicio`, mientras que la tabla `alquiler_servicio` permite registrar los diferentes servicios seleccionados para cada alquiler.

De esta manera, se evita almacenar varios teléfonos, servicios o pagos en una sola columna, facilitando la consulta y administración de la información.

---

### **2. SEGUNDA FORMA NORMAL (2FN)**

La segunda forma normal establece que todos los atributos que no forman parte de una clave deben depender de la clave primaria completa y no solamente de una parte de ella. Para cumplir esta condición, la tabla debe encontrarse previamente en la primera forma normal.

En el sistema propuesto, esta condición se aplica especialmente a la tabla `alquiler_servicio`, que utiliza una clave primaria compuesta por `id_alquiler` e `id_servicio`.

El campo `precio_acordado` representa el precio del servicio seleccionado para un alquiler específico, por lo que depende de la combinación completa de ambas claves y permite conservar el precio histórico aunque posteriormente cambie el precio actual del servicio.

Además, las tablas `cuarto`, `inquilino`, `alquiler`, `servicio`, `pago`, `garantia` y `parqueo` mantienen sus propios registros identificados mediante claves primarias, evitando mezclar información de distintas entidades.

---

### **3. TERCERA FORMA NORMAL (3FN)**

La tercera forma normal establece que los atributos que no son claves deben depender directamente de la clave primaria y no de otros atributos que no sean claves.

En la base de datos propuesta, la información se distribuye en tablas independientes para representar cada entidad del sistema. Por ejemplo, los datos personales se almacenan en `inquilino`, las características de los cuartos en `cuarto` y los precios actuales de los servicios en `servicio`.

Los pagos se registran en la tabla `pago`, relacionada con el alquiler correspondiente mediante una clave foránea. De igual manera, las garantías se almacenan en `garantia` y los servicios contratados se relacionan mediante `alquiler_servicio`.

Esta separación evita repetir información innecesariamente y permite actualizar los datos de cada entidad sin modificar registros que no le corresponden. También facilita mantener la consistencia de la información mediante claves primarias y foráneas.

---

### **CONCLUSIÓN DE LA NORMALIZACIÓN**

La aplicación de la primera, segunda y tercera forma normal permite obtener una estructura de base de datos organizada, con menor redundancia y relaciones correctamente definidas. Esto facilita la administración de los cuartos, inquilinos, alquileres, garantías, servicios adicionales, pagos y espacios de parqueo, además de permitir que el sistema crezca sin comprometer la integridad de los datos.
