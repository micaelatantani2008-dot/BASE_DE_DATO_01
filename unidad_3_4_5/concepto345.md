# APLICACIÓN DE LA NORMALIZACIÓN EN EL DISEÑO LÓGICO

La normalización permite organizar la información de una base de datos para reducir la redundancia, mantener la integridad de los datos y evitar anomalías durante la inserción, actualización y eliminación de registros. En el sistema de gestión de alquiler de cuartos, desarrollado con MariaDB/MySQL, se organiza la información mediante tablas relacionadas que representan las casas, los cuartos, las personas, los usuarios, los alquileres, los servicios adicionales, los parqueos, las garantías y los pagos.

Para el diseño lógico se consideran las tres primeras formas normales: primera forma normal (1FN), segunda forma normal (2FN) y tercera forma normal (3FN).

## 1. PRIMERA FORMA NORMAL (1FN)

La primera forma normal establece que cada campo debe contener un único valor y que no deben existir grupos de datos repetidos dentro de una misma tabla.

En el sistema de gestión de alquiler de cuartos, la información se distribuye en tablas específicas según la función que cumple cada entidad. Por ejemplo, la tabla `casa` almacena información de las casas administradas por el sistema, mientras que `cuarto` registra los cuartos disponibles. Por su parte, la tabla `persona` contiene los datos personales y `usuario` administra la información relacionada con las cuentas de acceso.

De igual manera, los alquileres se registran en `detalle_alquiler`, los servicios se identifican mediante `servicio` y las relaciones entre alquileres y servicios se gestionan mediante `alquiler_servicio`. Los pagos y sus conceptos de detalle se organizan en las tablas `pago` y `detalle_pago`, respectivamente.

Esta distribución permite registrar y consultar la información de manera estructurada, evitando almacenar varios servicios, cuartos o conceptos de pago dentro de un único campo. De esta forma, se facilita la administración de los datos y se cumple el principio de atomicidad establecido por la primera forma normal, siempre que los campos de cada tabla mantengan valores individuales.

## 2. SEGUNDA FORMA NORMAL (2FN)

La segunda forma normal establece que una tabla debe cumplir previamente con la primera forma normal y que cada atributo que no sea clave debe depender de la clave primaria completa, sin depender únicamente de una parte de ella.

En el sistema, las tablas utilizan identificadores para distinguir sus registros. Por ejemplo, `detalle_alquiler` utiliza `id_alquiler`, `pago` utiliza `id_pago`, `garantia` utiliza `id_garantia` y `asignacion_parqueo` utiliza `id_asignacion` como claves primarias.

Estas claves permiten identificar de manera individual cada alquiler, pago, garantía y asignación de parqueo. Las claves foráneas establecen las relaciones entre las tablas sin necesidad de repetir todos los datos de las entidades relacionadas.

Por ejemplo, `detalle_alquiler` se relaciona con `cuarto`, `persona` y `grupo_alquiler` mediante sus respectivas claves foráneas. Asimismo, `detalle_pago` se vincula con `pago`, mientras que `asignacion_parqueo` relaciona los registros correspondientes al parqueo, al alquiler y a la persona.

Esta organización favorece la independencia de los registros y evita mezclar información que corresponde a entidades diferentes. No obstante, el cumplimiento estricto de la segunda forma normal también requiere verificar que no existan dependencias parciales respecto de claves candidatas compuestas.

## 3. TERCERA FORMA NORMAL (3FN)

La tercera forma normal establece que una tabla debe cumplir con la segunda forma normal y que sus atributos que no son claves deben depender directamente de una clave candidata, sin depender transitivamente de otros atributos que no sean claves.

En el sistema de alquiler de cuartos, la información se distribuye en tablas que representan entidades y operaciones específicas. Por ejemplo, `persona` almacena los datos personales; `casa` identifica las casas administradas; `cuarto` registra los cuartos; y `usuario` mantiene la información correspondiente a las cuentas de acceso. La tabla `perfil` permite organizar los tipos de usuario, mientras que `usuario_casa` relaciona los usuarios con las casas que tienen asignadas.

Para administrar los alquileres, la tabla `grupo_alquiler` permite relacionar a una persona con una casa, y `detalle_alquiler` registra los alquileres de los cuartos correspondientes. Esta separación facilita la administración de los alquileres vinculados a una misma persona y casa.

Los servicios adicionales se organizan mediante `servicio` y `alquiler_servicio`. Además, `garantia` registra la información relacionada con las garantías, `pago` almacena los registros de pago y `detalle_pago` permite registrar sus conceptos. En el caso de los parqueos, `parqueo` y `asignacion_parqueo` permiten distinguir los espacios disponibles de las asignaciones realizadas.

El sistema también contempla la administración de varias casas y la asignación de usuarios a ellas. Esto permite separar la gestión de cada casa y organizar los servicios adicionales de acuerdo con las necesidades de su administración. Cuando se modifica un precio, es importante conservar el importe aplicado a la operación correspondiente para mantener el historial de los cobros.

Esta distribución reduce la repetición innecesaria de información y facilita las actualizaciones. Sin embargo, para confirmar formalmente el cumplimiento de la tercera forma normal, es necesario comprobar las dependencias funcionales de los atributos de cada tabla.

## CONCLUSIÓN DE LA NORMALIZACIÓN

La aplicación de las tres primeras formas normales constituye una base para organizar la información del sistema de gestión de alquiler de cuartos. La separación de las entidades y el uso de claves primarias y foráneas permiten establecer relaciones entre casas, cuartos, personas, usuarios, alquileres, servicios adicionales, parqueos, garantías y pagos.

Esta estructura facilita la consulta y el mantenimiento de la información, reduce la duplicidad de datos y contribuye a preservar la integridad de los registros. Asimismo, permite administrar varias casas dentro de un mismo sistema y mantener diferenciadas las operaciones relacionadas con cada una.

Por tanto, la normalización contribuye a que la base de datos sea más organizada y mantenible. La verificación definitiva de las formas normales debe realizarse considerando las columnas, las claves candidatas y las dependencias funcionales de la estructura implementada en MariaDB/MySQL.
