# IMPLEMENTACIÓN DEL DISEÑO FÍSICO EN SQL SERVER

El diseño físico permite llevar a SQL Server la estructura definida para el **Sistema de Gestión de Alquiler de Cuartos**. En esta etapa se establecen las tablas, los tipos de datos, las claves y las restricciones necesarias para almacenar y administrar la información de los cuartos, los inquilinos, los alquileres, las garantías, los servicios adicionales, los espacios de parqueo y los pagos.

La base de datos tiene como finalidad facilitar el control de los siete cuartos disponibles en la vivienda, mantener un registro histórico de los alquileres y sus precios, administrar los servicios contratados y llevar un seguimiento de los pagos realizados por cada inquilino.

---

## **CREACIÓN DE LA BASE DE DATOS Y LAS TABLAS**

Se organiza en tablas relacionadas mediante claves primarias y foráneas, lo que permite mantener la integridad de la información y establecer relaciones entre los distintos elementos del sistema. El modelo contempla las siguientes tablas principales:

- **Cuartos:** la tabla `cuarto` almacena el número del cuarto, sus dimensiones, superficie, precio mensual de alquiler, monto de garantía y estado de disponibilidad. Se registran siete cuartos: uno de 3 × 3 metros, 3.5 × 3 metros y cinco de 4 × 4 metros. El precio inicial de alquiler es de Bs 450 mensuales por cuarto, con la posibilidad de modificarlo posteriormente.

- **Inquilinos:** la tabla `inquilino` contiene los datos personales de cada persona que alquila un cuarto, incluyendo nombre, apellido, carnet de identidad, teléfono, correo electrónico y dirección. Se podrán establecer restricciones para evitar registros duplicados, especialmente en el carnet de identidad.

- **Alquileres:** la tabla `alquiler` relaciona a los inquilinos con los cuartos seleccionados y registra la fecha de inicio, la fecha de finalización, el precio mensual acordado y el estado del alquiler. El precio se almacena en el propio registro del alquiler para conservar el importe original, aunque el administrador modifique posteriormente el precio actual del cuarto.

- **Garantías:** la tabla `garantia` permite registrar si el inquilino aceptó pagar la garantía, el monto acordado, la fecha de pago, la fecha de devolución y su estado. El importe dependerá del tamaño del cuarto y estará aproximadamente entre Bs 1.500 y Bs 2.000.

- **Servicios adicionales:** las tablas `servicio` y `alquiler_servicio` permiten administrar los servicios disponibles y relacionarlos con los alquileres. Los servicios iniciales son electrodoméstico, internet y parqueo, cada uno con un precio de Bs 50 mensuales. También se conservará el precio aplicado al momento de la contratación.

- **Parqueos:** la tabla `parqueo` registra los cinco espacios disponibles para vehículos, identificando cada espacio y su estado, que puede ser disponible u ocupado. Se deberán implementar validaciones para impedir que se asignen más de cinco espacios simultáneamente.

- **Métodos de pago:** la tabla `metodo_pago` almacena los métodos admitidos por el sistema: pago mediante QR y pago en efectivo.

- **Pagos:** la tabla `pago` registra los pagos realizados por los inquilinos, incluyendo el alquiler correspondiente, la fecha, el monto, el mes y el año pagados, el método de pago y el comprobante cuando se trate de una operación mediante QR.

Para la implementación se utilizarán tipos de datos compatibles con SQL Server, como `INT` para identificadores, `VARCHAR` para cadenas de texto, `DECIMAL` para importes monetarios, `DATE` para las fechas y `BIT` para valores de tipo verdadero o falso, cuando corresponda.

Las claves primarias identificarán de forma única cada registro, mientras que las claves foráneas establecerán las relaciones entre las tablas. También se podrán utilizar restricciones `UNIQUE`, `NOT NULL` y `CHECK` para evitar duplicaciones, exigir campos obligatorios y validar los valores ingresados.

Asimismo, se deberán implementar controles para impedir que un mismo cuarto tenga alquileres activos durante periodos superpuestos y para garantizar que no se asignen más de cinco espacios de parqueo al mismo tiempo.

---

## **REGISTRO Y ADMINISTRACIÓN DE LOS ALQUILERES**

El sistema permitirá registrar los alquileres relacionando cada inquilino con el cuarto seleccionado. Al momento de crear un alquiler, se guardarán las fechas correspondientes, el precio mensual acordado y el estado del contrato.

La tabla `cuarto` mantendrá el precio vigente de cada habitación, mientras que la tabla `alquiler` conservará el precio establecido en cada contrato. De esta forma, las modificaciones futuras realizadas por el administrador no alterarán el historial de los alquileres anteriores.

Los cuartos podrán presentar los estados disponible, alquilado, reservado o en mantenimiento. Esta información permitirá identificar cuáles se encuentran libres y cuáles no pueden asignarse a un nuevo inquilino.

---

## **REGISTRO DE SERVICIOS ADICIONALES Y CÁLCULO DEL ALQUILER**

El sistema permitirá seleccionar uno o varios servicios adicionales para cada alquiler. Inicialmente, se contemplan los siguientes precios mensuales:

- **Electrodoméstico:** Bs 50.
- **Internet:** Bs 50.
- **Parqueo:** Bs 50.

El importe mensual se calculará sumando el precio acordado del cuarto y los servicios contratados. Por ejemplo, si un inquilino alquila un cuarto por Bs 450 y selecciona internet y parqueo, el cálculo será el siguiente:

**Bs 450 + Bs 50 + Bs 50 = Bs 550 mensuales.**

El sistema deberá conservar los precios aplicados a los servicios al momento de su contratación, evitando que las modificaciones posteriores de las tarifas alteren los importes históricos.

---

## **INSERCIÓN DE DATOS INICIALES**

Después de crear las tablas, se deberán insertar los datos iniciales necesarios para el funcionamiento del sistema.

La carga inicial incluirá los siete cuartos de la vivienda, con sus respectivas dimensiones y superficies:

- **Cuarto 1:** 3 × 3 metros, con una superficie de 9 m².
- **Cuarto 2:** 3,5 × 3 metros, con una superficie de 10,5 m².
- **Cuartos 3 al 7:** 4 × 4 metros, con una superficie de 16 m² cada uno.

Cada cuarto tendrá un precio inicial de Bs 450 mensuales. También se registrarán los tres servicios adicionales con sus tarifas iniciales de Bs 50 mensuales y los cinco espacios de parqueo, que comenzarán con estado disponible.

Los métodos de pago mediante QR y efectivo se incorporarán como datos iniciales en la tabla `metodo_pago`.

Posteriormente, los registros de inquilinos, alquileres, garantías y pagos se añadirán conforme se utilice el sistema. De esta manera, la base de datos permitirá mantener un historial de las operaciones realizadas.

---

## **EJECUCIÓN**

La implementación se realizará mediante un script SQL compatible con SQL Server, que contendrá las instrucciones necesarias para crear la base de datos, definir las tablas, establecer sus relaciones y cargar los datos iniciales.

El script podrá ejecutarse desde SQL Server Management Studio utilizando una cuenta con los permisos necesarios para crear bases de datos y tablas.

Una vez implementada la estructura, la base de datos permitirá administrar la información de los cuartos, registrar los alquileres, controlar la disponibilidad, gestionar las garantías, calcular los importes de los servicios adicionales y llevar el historial de los pagos realizados por los inquilinos.

Con esta organización se busca mantener la información centralizada, reducir errores de registro y facilitar la administración de los alquileres de la vivienda.
