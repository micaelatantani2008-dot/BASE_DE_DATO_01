# IMPLEMENTACIÓN DEL DISEÑO FÍSICO EN MARIADB

El diseño físico permite implementar en MariaDB la estructura de la base de datos del **Sistema de Gestión de Alquiler de Cuartos**. En esta etapa se organizan las tablas, los campos, los tipos de datos y las relaciones necesarias para almacenar y administrar la información del sistema.

La base de datos utilizada es `alquiler_cuartos`, que se administra mediante DBeaver y se ejecuta localmente a través de MariaDB en XAMPP. Esta estructura sirve de soporte para el sistema web desarrollado con PHP, destinado a gestionar las casas, los cuartos, los usuarios, los alquileres, los servicios adicionales, los parqueos y los pagos.

A diferencia de una estructura diseñada para una sola vivienda, el sistema contempla la administración de varias casas, con usuarios y administradores asociados a las viviendas que les corresponden. Esto permite organizar la información y mantener separados los datos que pertenecen a cada casa.

---

## CREACIÓN Y ORGANIZACIÓN DE LAS TABLAS

La base de datos está organizada en tablas relacionadas mediante identificadores y relaciones entre registros. Su estructura contempla 19 tablas principales, distribuidas según las funciones administrativas y operativas del sistema.

Las tablas identificadas son las siguientes:

- **Casa (`casa`):** almacena la información de las viviendas administradas por el sistema. Permite organizar los cuartos y asociar la administración correspondiente a cada casa.

- **Cuarto (`cuarto`):** contiene la información de las habitaciones disponibles para alquiler, sus características y los datos relacionados con su administración y disponibilidad.

- **Persona (`persona`):** almacena los datos personales de las personas registradas en el sistema. Esta información se relaciona con los usuarios y permite evitar la repetición innecesaria de datos personales en diferentes registros.

- **Usuario (`usuario`):** contiene la información de acceso al sistema, incluyendo el nombre de usuario, la contraseña almacenada mediante un mecanismo de hash, el estado de la cuenta y otros datos de control.

- **Perfil (`perfil`):** define los perfiles de acceso disponibles. Se contemplan los perfiles de superadministrador, administrador e inquilino, de acuerdo con la estructura de permisos del sistema.

- **Usuario por casa (`usuario_casa`):** relaciona a los usuarios con las casas que tienen asignadas. Esta tabla permite establecer a qué vivienda corresponde la administración de cada usuario.

- **Alquiler (`alquiler`):** registra la información de los alquileres y relaciona los cuartos con las personas o registros correspondientes. Constituye una parte central del control de ocupación y de la administración de los contratos.

- **Detalle de alquiler (`detalle_alquiler`):** permite organizar la información complementaria asociada a los alquileres, de acuerdo con la estructura definida en la base de datos.

- **Garantía (`garantia`):** almacena la información relacionada con las garantías de los alquileres, permitiendo llevar el control de los importes y de los registros correspondientes a esta obligación contractual.

- **Servicio (`servicio`):** contiene el catálogo de servicios adicionales que pueden ofrecerse a los inquilinos. El sistema contempla la posibilidad de administrar servicios y precios según las necesidades de cada casa.

- **Alquiler por servicio (`alquiler_servicio`):** relaciona los alquileres con los servicios contratados. Esta relación permite asociar uno o varios servicios a un alquiler y organizar la información de los adicionales.

- **Parqueo (`parqueo`):** registra los espacios destinados al estacionamiento de vehículos y la información necesaria para administrarlos.

- **Asignación de parqueo (`asignacion_parqueo`):** permite relacionar los espacios de parqueo con las asignaciones correspondientes, facilitando el control de su utilización.

- **Historial de precios (`historial_precio`):** permite registrar información histórica de los precios para mantener un seguimiento de las variaciones realizadas en las tarifas.

- **Pago (`pago`):** almacena los registros principales de los pagos efectuados en el sistema, permitiendo llevar el control de las operaciones económicas relacionadas con los alquileres.

- **Detalle de pago (`detalle_pago`):** permite organizar el detalle de los conceptos económicos asociados a un pago, de acuerdo con la estructura de la base de datos.

- **Recibo (`recibo`):** está destinado a almacenar la información correspondiente a los recibos vinculados con los pagos registrados.

- **Sesión (`sesion`):** registra las sesiones de acceso de los usuarios, incluyendo información de control como el token, las fechas de inicio y expiración y el estado de la sesión.

- **Bitácora de acceso (`bitacora_acceso`):** permite mantener un registro de los eventos relacionados con el acceso de los usuarios, contribuyendo al seguimiento de los intentos de inicio de sesión.

- **Bitácora de auditoría (`bitacora_auditoria`):** está destinada al registro de eventos de auditoría para facilitar el seguimiento de las operaciones realizadas en el sistema.

La estructura utiliza tipos de datos compatibles con MariaDB, seleccionados según la naturaleza de cada campo. Entre ellos pueden encontrarse tipos enteros para identificadores, cadenas de texto para datos descriptivos, tipos decimales para importes monetarios, tipos de fecha y hora para registrar eventos temporales y valores numéricos o lógicos para estados y controles.

Las claves primarias permiten identificar los registros de forma única, mientras que las claves foráneas establecen relaciones entre las tablas. Asimismo, las restricciones de integridad permiten controlar los datos almacenados cuando están definidas en la estructura correspondiente.

---

## ADMINISTRACIÓN DE USUARIOS Y PERMISOS

El sistema cuenta con una estructura de usuarios y perfiles que permite diferenciar las funciones de administración.

Se contemplan tres perfiles principales:

- **Superadministrador:** dispone del perfil de mayor nivel para las tareas generales de administración del sistema.
- **Administrador:** gestiona la información y las operaciones correspondientes a la casa que tiene asignada.
- **Inquilino:** representa el perfil previsto para las personas que alquilan habitaciones, sin acceso directo habilitado para iniciar sesión en la configuración actual de los perfiles.

La relación entre usuarios y casas se organiza mediante la tabla `usuario_casa`. De esta manera, la administración puede vincularse con una vivienda determinada y separar la información según la casa correspondiente.

Para el inicio de sesión se utiliza el procedimiento almacenado `sp_iniciar_sesion`, que participa en la validación de las credenciales, el control del estado de la cuenta, los intentos fallidos y la creación de sesiones. Las contraseñas se verifican mediante hash SHA-256, de acuerdo con la implementación actual.

La aplicación web desarrollada en PHP se comunica con MariaDB para realizar las operaciones de autenticación y administración.

---

## REGISTRO Y ADMINISTRACIÓN DE LOS ALQUILERES

El sistema organiza la información de los cuartos y los alquileres mediante tablas relacionadas. Esta estructura permite registrar las operaciones de alquiler y mantener vinculados los datos correspondientes a las habitaciones y las personas involucradas.

La administración de varias casas requiere que las operaciones se realicen considerando la vivienda a la que pertenecen. Esto permite que cada administrador trabaje con la información correspondiente a su casa, respetando la separación de los datos del sistema.

La tabla `cuarto` mantiene la información de las habitaciones, mientras que la tabla `alquiler` permite registrar las operaciones de alquiler. Las tablas complementarias, como `detalle_alquiler` y `garantia`, permiten organizar la información relacionada con estas operaciones.

Además, la tabla `historial_precio` forma parte de la estructura destinada al seguimiento de las variaciones de precios. Esto resulta importante para la administración de tarifas a lo largo del tiempo.

Las validaciones específicas de disponibilidad, superposición de contratos y cambios de estado deben corresponder a las reglas que estén implementadas en la base de datos y en la aplicación.

---

## ADMINISTRACIÓN DE SERVICIOS ADICIONALES Y PARQUEOS

El sistema contempla la administración de servicios adicionales asociados a los alquileres. La tabla `servicio` almacena el catálogo de servicios, mientras que `alquiler_servicio` permite relacionar los servicios con los alquileres correspondientes.

La administración de precios debe considerar las particularidades de cada casa. Por este motivo, los precios configurados por un administrador para sus servicios y adicionales deben mantenerse diferenciados de los correspondientes a otras viviendas cuando así lo establece la lógica del sistema.

La tabla `historial_precio` permite organizar el registro de los cambios de tarifas. Para conservar correctamente la información histórica, los importes aplicados a cada contratación deben quedar registrados en los datos correspondientes a la operación.

En cuanto a los espacios de estacionamiento, la tabla `parqueo` contiene su información y `asignacion_parqueo` permite administrar las asignaciones. Esta organización facilita el seguimiento de los espacios utilizados y de las relaciones entre las asignaciones y los registros correspondientes.

---

## REGISTRO Y CONTROL DE LOS PAGOS

La gestión económica se organiza mediante las tablas `pago` y `detalle_pago`. La primera almacena los registros principales de los pagos, mientras que la segunda permite estructurar el detalle de los conceptos asociados a cada operación.

La tabla `recibo` complementa esta estructura y está destinada a los registros relacionados con los comprobantes de pago.

Esta organización permite preparar el sistema para consultar los pagos y sus conceptos, así como generar recibos con información relacionada con el alquiler, los servicios y los adicionales que correspondan.

La funcionalidad de descarga del recibo en formato PDF y su posterior distribución por WhatsApp forma parte de las tareas de desarrollo pendientes. Por tanto, no debe presentarse como una funcionalidad finalizada hasta que esté implementada y probada en la aplicación.

---

## CONTROL DE SESIONES Y AUDITORÍA

El sistema incorpora tablas destinadas al control de los accesos y al seguimiento de las operaciones.

La tabla `sesion` permite administrar los registros de sesión y almacenar información como el token, la fecha de inicio, la fecha de expiración y el estado de la sesión.

Por otra parte, `bitacora_acceso` permite registrar eventos relacionados con los intentos de acceso. Esta información contribuye al seguimiento de la autenticación y al control de los usuarios.

La tabla `bitacora_auditoria` complementa esta estructura y está destinada a registrar eventos relevantes para la auditoría del sistema.

Estas tablas proporcionan una base para el seguimiento de las actividades, la revisión de los accesos y la mejora del control administrativo.

---

## INSERCIÓN Y ADMINISTRACIÓN DE DATOS

La base de datos contiene registros que permiten organizar las casas, los cuartos, los usuarios y los demás elementos necesarios para el funcionamiento del sistema.

Los datos se almacenan en las tablas correspondientes y se relacionan mediante sus identificadores. Esta organización permite mantener la información centralizada y facilita las consultas realizadas por la aplicación web.

A diferencia de una base de datos limitada a una sola vivienda, la estructura contempla varias casas y usuarios asociados a ellas. Por ello, la administración de los datos debe respetar las relaciones establecidas y las reglas de acceso correspondientes.

Los registros de alquileres, garantías, servicios, parqueos, pagos, recibos y sesiones se administran mediante sus respectivas tablas, de acuerdo con las operaciones realizadas en el sistema.

La información inicial y los datos de prueba deben mantenerse coherentes con la estructura real de la base de datos, evitando asumir cantidades fijas de habitaciones, precios únicos o tarifas globales cuando estos valores dependen de cada casa.

---

## EJECUCIÓN Y CONEXIÓN CON LA APLICACIÓN WEB

La base de datos `alquiler_cuartos` se administra mediante DBeaver y se ejecuta localmente utilizando MariaDB en XAMPP. Para la conexión con la aplicación se utiliza PHP, que permite procesar las solicitudes del sistema y ejecutar las operaciones correspondientes sobre la base de datos.

La conexión se configura mediante los archivos del proyecto, mientras que las operaciones de autenticación y administración se distribuyen entre los archivos PHP y los procedimientos almacenados que correspondan.

La implementación del sistema se desarrolla de manera progresiva, verificando el funcionamiento de las operaciones y la relación entre la aplicación web y la base de datos.

Antes de publicar el sistema en producción, será necesario comprobar la integridad de los datos, los permisos de los usuarios, la seguridad de las credenciales, la correcta configuración del servidor y el funcionamiento de las operaciones principales.

Con esta organización se busca centralizar la información, facilitar la administración de varias casas, mantener un control ordenado de los alquileres y los pagos, y establecer una estructura que permita continuar ampliando las funcionalidades del sistema.

En conclusión, el diseño físico de `alquiler_cuartos` constituye la base de almacenamiento del Sistema de Gestión de Alquiler de Cuartos y permite relacionar la información administrativa y operativa necesaria para su funcionamiento.
