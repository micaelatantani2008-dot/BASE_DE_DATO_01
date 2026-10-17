# **UNIDAD 1 – ENTREVISTA Y DISEÑO LÓGICO DE LA BASE DE DATOS**

---

## **1. INTRODUCCIÓN**

El presente proyecto tiene como finalidad desarrollar una base de datos para la gestión de alquiler de cuartos, permitiendo administrar de manera organizada la información de los cuartos, inquilinos, alquileres, garantías, servicios adicionales, parqueos y pagos realizados.

Mediante el diseño de una base de datos relacional, se busca facilitar el registro y control de la información, evitar la duplicación de datos y mejorar la administración de los alquileres.

---

## **2. ENTREVISTA AL ENCARGADO DEL ALQUILER**

**Entrevistador:** ¿Cuántos cuartos se encuentran disponibles para alquilar?

**Encargado:** Actualmente contamos con siete cuartos de diferentes tamaños, cada uno con un precio mensual establecido.

**Entrevistador:** ¿Qué información se registra de los inquilinos?

**Encargado:** Se registra su nombre, apellido, número de carnet de identidad, teléfono, correo electrónico y dirección.

**Entrevistador:** ¿Cómo se controlan los alquileres?

**Encargado:** Se registra el cuarto asignado a cada inquilino, la fecha de inicio, la fecha de finalización y el precio mensual acordado. También se controla si el cuarto está disponible, alquilado, reservado o en mantenimiento.

**Entrevistador:** ¿Se solicita una garantía para alquilar un cuarto?

**Encargado:** La garantía es opcional. Cuando se solicita, se registra el monto, la aceptación, la fecha de pago y la fecha de devolución.

**Entrevistador:** ¿Existen servicios adicionales?

**Encargado:** Sí. Se ofrecen servicios como internet, electrodomésticos y parqueo. Cada servicio tiene un precio mensual y el inquilino puede elegir los que necesite.

**Entrevistador:** ¿Cómo se realizan los pagos?

**Encargado:** Los pagos pueden realizarse en efectivo o mediante QR. Se registra el monto, la fecha, el mes y el año correspondientes. Si el pago se realiza mediante QR, también se puede guardar el comprobante.

**Entrevistador:** ¿Cómo se controla la disponibilidad del parqueo?

**Encargado:** Se cuenta con un máximo de cinco espacios de parqueo y se registra cuáles están disponibles y cuáles se encuentran ocupados.

---

## **3. REQUERIMIENTOS DEL SISTEMA**

A partir de la entrevista, se identificaron los siguientes requerimientos:

- Registrar y administrar los cuartos disponibles para alquiler.
- Registrar los datos personales de los inquilinos.
- Controlar los contratos y períodos de alquiler.
- Registrar las garantías y su estado.
- Administrar los servicios adicionales y sus precios.
- Registrar los pagos mensuales y sus respectivos comprobantes.
- Controlar la disponibilidad de los espacios de parqueo.
- Evitar que un mismo cuarto tenga alquileres activos en períodos que se superpongan.
- Conservar los precios acordados en cada alquiler, aunque posteriormente cambien los precios actuales.

---

## **4. DISEÑO LÓGICO (DIAGRAMA RELACIONAL)**

El diseño lógico representa la estructura de la base de datos mediante tablas relacionadas entre sí. Cada tabla contiene campos que permiten almacenar información específica, utilizando claves primarias (PK) para identificar los registros y claves foráneas (FK) para establecer las relaciones.

### **4.1. TABLAS PRINCIPALES**

| Tabla | Descripción |
|---|---|
| **CUARTO** | Almacena los datos, dimensiones, precio y estado de cada cuarto. |
| **INQUILINO** | Contiene la información personal de los inquilinos. |
| **ALQUILER** | Registra los alquileres, sus fechas y el precio acordado. |
| **GARANTIA** | Almacena los datos de las garantías asociadas a los alquileres. |
| **SERVICIO** | Registra los servicios adicionales y sus precios mensuales. |
| **ALQUILER_SERVICIO** | Relaciona los alquileres con los servicios seleccionados. |
| **PAGO** | Registra los pagos mensuales, métodos de pago y comprobantes. |
| **PARQUEO** | Controla los espacios de parqueo y su disponibilidad. |

### **4.2. RELACIONES ENTRE LAS TABLAS**

Las principales relaciones del modelo son las siguientes:

- Un cuarto puede tener varios alquileres a lo largo del tiempo.
- Un inquilino puede realizar varios alquileres.
- Un alquiler puede tener una garantía.
- Un alquiler puede incluir varios servicios adicionales.
- Un servicio puede estar asociado a diferentes alquileres.
- Un alquiler puede registrar varios pagos.
- Un espacio de parqueo puede asignarse a un alquiler, siempre que se encuentre disponible.

### **4.3. DIAGRAMA RELACIONAL**

En esta sección se incorporará el diagrama relacional de la base de datos, donde se visualizarán las tablas, sus campos, las claves primarias (PK), las claves foráneas (FK) y las relaciones entre ellas.

**[INSERTAR AQUÍ LA IMAGEN DEL DIAGRAMA RELACIONAL]**

---

## **5. CONCLUSIÓN**

La elaboración del diseño lógico permite organizar la información necesaria para administrar los alquileres de cuartos de forma estructurada. La identificación de las tablas y sus relaciones constituye una base para la posterior implementación de la base de datos, facilitando el control de los inquilinos, alquileres, servicios, garantías, pagos y espacios de parqueo.


