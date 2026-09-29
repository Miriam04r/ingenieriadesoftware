# Especificación de requisitos

**Sistema:** EmpeñoControl  

**Autor:** Miriam Gómez Mariscal  

**Fecha de la última actualización:** 28/09/2026  

---

## 1. Propósito y alcance

### Propósito del documento

Este documento define los requisitos funcionales y no funcionales del sistema EmpeñoControl. Su objetivo es establecer qué debe hacer el sistema y qué características debe tener para facilitar el control de los clientes, préstamos, empeños, pagos e intereses de una casa de empeño pequeña.

### Dentro del alcance

- Calcula intereses ingresando los datos del cliente
- Hace un balance de cuanto dinero tiene prestado el owner y cuánto dinero le está generando
- Permite hacer un registro manual de cada cliente y empeño con su información correspondiente
- Subraya a los empeños que están vencidos de color rojo y los manda arriba de la lista manteniendo al más antiguo al principio
- Mantiene un historial de las modificaciones realizadas en los registros

### Explícitamente fuera del alcance

- No calcula el impuesto de cada cliente por si solo, si no que cuando se necesita saber se ingresan los datos y se calcula
- No manda un aviso de cuando un cliente se atrasó con el pago
- El estado de los pagos no se actualiza automáticamente

---

## 2. Usuarios y su contexto

| Usuario | Qué hace hoy sin el sistema | Qué espera del sistema |
| ------- | --------------------------- | ---------------------- |
| Owner | Revisa los empeños activos, pagos, deudas y empeños vencidos. Registra información en libretas y fichas. | Tener control de clientes, préstamos, empeños y pagos, consultar deudas y revisar los empeños vencidos. |
| Employee | Atiende clientes, registra empeños y recibe pagos. Actualmente registra la información manualmente. | Registrar clientes, préstamos, empeños y pagos de manera sencilla y consultar la información necesaria. |

### Conflictos identificados entre usuarios

El Owner necesita mantener control sobre las operaciones y autorizar los préstamos mayores a $50,000 pesos, mientras que el Employee necesita poder registrar los préstamos y pagos para atender a los clientes.

---

## 3. Requisitos funcionales

### 3.1 Resumen

| ID | Nombre | Prioridad | Origen |
| --- | --- | --- | --- |
| RF-001 | Registro de clientes | Imprescindible | Entrevista |
| RF-002 | Registro de préstamos y empeños | Imprescindible | Entrevista |
| RF-003 | Registro de pagos | Imprescindible | Entrevista |
| RF-004 | Cálculo de intereses | Imprescindible | Entrevista |
| RF-005 | Consulta de empeños y deudas | Imprescindible | Entrevista |
| RF-006 | Control de empeños vencidos | Imprescindible | Entrevista |
| RF-007 | Autorización de préstamos mayores a $50,000 | Imprescindible | Entrevista |
| RF-008 | Registro de cambios en la información | Importante | Entrevista |

### 3.2 Fichas

#### RF-001 · Registro de clientes

| Campo | Contenido |
| --- | --- |
| **Descripción** | El sistema permitirá registrar y consultar la información de los clientes de la casa de empeño. |
| **Origen** | Entrevista con el Owner. |
| **Prioridad** | Imprescindible |
| **Criterio de aceptación** | Al registrar un cliente con la información requerida, el sistema deberá guardar sus datos y permitir consultarlos posteriormente. |
| **Relacionado con** | RF-002, RF-005 |

#### RF-002 · Registro de préstamos y empeños

| Campo | Contenido |
| --- | --- |
| **Descripción** | El sistema permitirá registrar préstamos y los objetos que quedan como garantía del préstamo. |
| **Origen** | Entrevista con el Owner. |
| **Prioridad** | Imprescindible |
| **Criterio de aceptación** | Al registrar un préstamo con los datos requeridos y su objeto de garantía, el sistema deberá guardar la información y relacionarla con el cliente correspondiente. |
| **Relacionado con** | RF-001, RF-004, RF-006, RF-007 |

#### RF-003 · Registro de pagos

| Campo | Contenido |
| --- | --- |
| **Descripción** | El sistema permitirá registrar los pagos realizados por los clientes y asociarlos con el empeño correspondiente. |
| **Origen** | Entrevista con el Owner. |
| **Prioridad** | Imprescindible |
| **Criterio de aceptación** | Al registrar un pago válido, el sistema deberá guardarlo y mostrarlo asociado al empeño correspondiente. |
| **Relacionado con** | RF-002, RF-004, RF-005 |

#### RF-004 · Cálculo de intereses

| Campo | Contenido |
| --- | --- |
| **Descripción** | El sistema calculará los intereses de un empeño de acuerdo con los días transcurridos desde el último pago y la información registrada del préstamo. |
| **Origen** | Entrevista con el Owner. |
| **Prioridad** | Imprescindible |
| **Criterio de aceptación** | Al consultar un empeño, el sistema deberá mostrar el interés correspondiente de acuerdo con los días transcurridos desde el último pago. |
| **Relacionado con** | RF-002, RF-003, RF-005 |

#### RF-005 · Consulta de empeños y deudas

| Campo | Contenido |
| --- | --- |
| **Descripción** | El sistema permitirá consultar los empeños activos, los pagos realizados y las deudas pendientes de los clientes. |
| **Origen** | Entrevista con el Owner. |
| **Prioridad** | Imprescindible |
| **Criterio de aceptación** | Al consultar un cliente, el sistema deberá mostrar sus empeños, pagos registrados y deudas pendientes. |
| **Relacionado con** | RF-001, RF-002, RF-003, RF-004, RF-006 |

#### RF-006 · Control de empeños vencidos

| Campo | Contenido |
| --- | --- |
| **Descripción** | El sistema permitirá identificar los empeños que llevan más de tres meses sin pagar intereses y distinguirlos de los empeños activos. |
| **Origen** | Entrevista con el Owner. |
| **Prioridad** | Imprescindible |
| **Criterio de aceptación** | Cuando un empeño tenga más de tres meses sin registrar un pago de intereses, el sistema deberá permitir identificarlo como vencido o inactivo. |
| **Relacionado con** | RF-003, RF-005 |

#### RF-007 · Autorización de préstamos mayores a $50,000

| Campo | Contenido |
| --- | --- |
| **Descripción** | El sistema deberá solicitar la autorización del Owner antes de completar un préstamo mayor a $50,000 pesos cuando sea registrado por el Employee. |
| **Origen** | Entrevista con el Owner. |
| **Prioridad** | Imprescindible |
| **Criterio de aceptación** | Si el Employee intenta registrar un préstamo mayor a $50,000 pesos, el sistema deberá solicitar la autorización del Owner antes de completar el registro. |
| **Relacionado con** | RF-002 |

#### RF-008 · Registro de cambios en la información

| Campo | Contenido |
| --- | --- |
| **Descripción** | El sistema permitirá conservar un registro de las modificaciones realizadas en la información de clientes, préstamos y pagos para poder revisar cambios anteriores. |
| **Origen** | Entrevista con el Owner. |
| **Prioridad** | Importante |
| **Criterio de aceptación** | Cuando se modifique información de un cliente, préstamo o pago, el sistema deberá conservar el registro del cambio para permitir su revisión posterior. |
| **Relacionado con** | RF-001, RF-002, RF-003 |

---

## 4. Requisitos no funcionales

### 4.1 Resumen

| ID | Atributo | Nombre | Prioridad | Origen |
| --- | --- | --- | --- | --- |
| RNF-REN-001 | Rendimiento | Tiempo de consulta | Importante | Derivado del tipo de sistema |
| RNF-SEG-001 | Seguridad | Control de acceso | Imprescindible | Entrevista |
| RNF-USA-001 | Usabilidad | Facilidad de uso | Imprescindible | Entrevista |
| RNF-CON-001 | Confiabilidad | Conservación de información | Imprescindible | Entrevista |

### 4.2 Fichas

#### RNF-REN-001 · Tiempo de consulta

| Campo | Contenido |
| --- | --- |
| **Atributo de calidad** | Rendimiento |
| **Descripción** | El sistema deberá mostrar la información solicitada por el usuario en un tiempo máximo de 3 segundos. |
| **Métrica** | Tiempo entre la solicitud de una consulta y la visualización de los resultados. |
| **Origen** | Derivado del tipo de sistema: sistema de información con consultas frecuentes durante la atención a clientes. |
| **Prioridad** | Importante |
| **Por qué importa** | El Owner y el Employee necesitan consultar rápidamente la información de los clientes, préstamos y pagos durante la atención. |
| **Afecta a** | RF-001, RF-002, RF-003, RF-005, RF-006 |

#### RNF-SEG-001 · Control de acceso

| Campo | Contenido |
| --- | --- |
| **Atributo de calidad** | Seguridad |
| **Descripción** | El sistema deberá permitir diferenciar el acceso del Owner y del Employee de acuerdo con sus funciones. |
| **Métrica** | El 100% de las funciones que requieran autorización del Owner deberán solicitarla antes de completar la operación. |
| **Origen** | Entrevista con el Owner. |
| **Prioridad** | Imprescindible |
| **Por qué importa** | El Owner necesita mantener control sobre operaciones importantes, como los préstamos mayores a $50,000. |
| **Afecta a** | RF-007, RF-008 |

#### RNF-USA-001 · Facilidad de uso

| Campo | Contenido |
| --- | --- |
| **Atributo de calidad** | Usabilidad |
| **Descripción** | El sistema deberá ser fácil de utilizar para el Owner y el Employee durante las actividades diarias de la casa de empeño. |
| **Métrica** | Un usuario deberá poder registrar un cliente, préstamo o pago sin requerir asistencia externa después de recibir una explicación básica del sistema. |
| **Origen** | Entrevista con el Owner. |
| **Prioridad** | Imprescindible |
| **Por qué importa** | Tanto el Owner como el Employee utilizarán el sistema para registrar información y atender a los clientes. |
| **Afecta a** | RF-001, RF-002, RF-003, RF-005 |

#### RNF-CON-001 · Conservación de información

| Campo | Contenido |
| --- | --- |
| **Atributo de calidad** | Confiabilidad |
| **Descripción** | El sistema deberá conservar la información registrada de clientes, préstamos, empeños y pagos aunque el cliente deje de acudir al negocio. |
| **Métrica** | La información registrada deberá permanecer disponible después de cerrar y volver a abrir el sistema. |
| **Origen** | Entrevista con el Owner. |
| **Prioridad** | Imprescindible |
| **Por qué importa** | La información histórica es necesaria para consultar los préstamos, pagos y deudas de los clientes. |
| **Afecta a** | RF-001, RF-002, RF-003, RF-005, RF-006, RF-008 |

---

## 5. Casos de uso

### CU-01 · Registrar cliente

**Actor principal:** Owner / Employee

**Descripción:** Permite registrar la información de un nuevo cliente.

**Requisitos relacionados:** RF-001.

### CU-02 · Registrar préstamo y empeño

**Actor principal:** Owner / Employee

**Descripción:** Permite registrar un préstamo y el objeto que queda como garantía.

**Requisitos relacionados:** RF-002, RF-007.

### CU-03 · Registrar pago

**Actor principal:** Owner / Employee

**Descripción:** Permite registrar un pago realizado por un cliente y asociarlo con su empeño.

**Requisitos relacionados:** RF-003, RF-004.

### CU-04 · Consultar información de cliente

**Actor principal:** Owner / Employee

**Descripción:** Permite consultar los empeños, pagos y deudas asociadas a un cliente.

**Requisitos relacionados:** RF-001, RF-005.

### CU-05 · Consultar empeños vencidos

**Actor principal:** Owner

**Descripción:** Permite consultar los empeños que llevan más de tres meses sin pagar intereses.

**Requisitos relacionados:** RF-005, RF-006.

### CU-06 · Autorizar préstamo mayor a $50,000

**Actor principal:** Owner

**Descripción:** Permite al Owner autorizar un préstamo mayor a $50,000 pesos registrado por el Employee.

**Requisitos relacionados:** RF-007.

### CU-07 · Consultar historial de cambios

**Actor principal:** Owner

**Descripción:** Permite revisar los cambios realizados en la información de clientes, préstamos y pagos.

**Requisitos relacionados:** RF-008.

---

## 6. Trazabilidad

| Requisito | Origen | Caso de uso | Elemento del prototipo |
| --- | --- | --- | --- |
| RF-001 | Entrevista | CU-01 Registrar cliente | Pantalla de clientes |
| RF-002 | Entrevista | CU-02 Registrar préstamo y empeño | Pantalla de préstamos |
| RF-003 | Entrevista | CU-03 Registrar pago | Pantalla de pagos |
| RF-004 | Entrevista | CU-03 Registrar pago | Cálculo de intereses |
| RF-005 | Entrevista | CU-04 Consultar información de cliente | Pantalla de consulta |
| RF-006 | Entrevista | CU-05 Consultar empeños vencidos | Pantalla de empeños vencidos |
| RF-007 | Entrevista | CU-06 Autorizar préstamo mayor a $50,000 | Pantalla de autorización |
| RF-008 | Entrevista | CU-07 Consultar historial de cambios | Pantalla de historial |
| RNF-REN-001 | Derivado del tipo de sistema | CU-04 Consultar información de cliente | Pantallas de consulta |
| RNF-SEG-001 | Entrevista | CU-06 Autorizar préstamo mayor a $50,000 | Control de acceso |
| RNF-USA-001 | Entrevista | CU-01, CU-02, CU-03 | Interfaz del sistema |
| RNF-CON-001 | Entrevista | CU-04, CU-05, CU-07 | Base de datos / almacenamiento |

---

## 7. Registro de cambios

| Fecha | Requisito | Qué cambió | Por qué |
| --- | --- | --- | --- |
| 28/09/2026 | RF-001 a RF-008 | Se agregaron los requisitos funcionales obtenidos de la entrevista. | Se realizó la entrevista con el Owner y se identificaron las funciones principales del sistema. |
| 28/09/2026 | RNF-REN-001 a RNF-CON-001 | Se agregaron requisitos no funcionales relacionados con rendimiento, seguridad, usabilidad y confiabilidad. | Se identificaron las características necesarias para el funcionamiento del sistema. |

---

## Antes de entregar

- [x] Todos los requisitos tienen identificador único y ninguno está repetido.
- [x] Cada requisito expresa una sola idea.
- [x] Cada requisito funcional tiene criterio de aceptación comprobable.
- [x] Cada requisito no funcional tiene una métrica.
- [x] El campo Origen distingue los requisitos obtenidos de la entrevista de los derivados.
- [x] Hay requisitos no funcionales para los atributos de calidad identificados.
- [x] Ningún requisito impone una solución técnica específica.
- [x] Todos los requisitos caben dentro del alcance declarado.
- [x] La tabla de trazabilidad está completa.
- [ ] La dupla revisó el documento y su revisión está registrada.
