# Especificación de requisitos

**Sistema:** EmpeñoControl
**Autor:** Miriam Gómez Mariscal
**Fecha de la última actualización:** 28/09/2026

---

## 1. Propósito y alcance

**Propósito del documento:**

Este documento define los requisitos funcionales y no funcionales del sistema EmpeñoControl. Está dirigido a las personas involucradas en el desarrollo y revisión del sistema, principalmente al Owner y al Employee de la casa de empeño. Su objetivo es establecer de manera clara qué debe hacer el sistema y cuáles son las características que debe cumplir.

**Alcance del sistema:**

EmpeñoControl permitirá registrar y consultar clientes, préstamos o empeños, objetos dejados como garantía y pagos realizados. También permitirá calcular los intereses de acuerdo con los días transcurridos desde el último pago, consultar adeudos y refrendos, e identificar los empeños que llevan más de tres meses sin pago.

El sistema tendrá dos tipos de usuario: Owner y Employee. El Owner podrá supervisar la información y autorizar operaciones mayores a $50,000. El Employee podrá realizar las operaciones permitidas para el registro y seguimiento de los empeños.

El sistema también conservará un historial de modificaciones para poder identificar cambios realizados sobre la información registrada.

**Fuera del alcance:**

* El sistema no determinará automáticamente la tasa de interés; esta deberá ser proporcionada de acuerdo con las reglas del negocio.
* El sistema no realizará cobros automáticos ni enviará alertas de pago.
* El sistema no procesará pagos con tarjeta ni transferencias bancarias; los pagos considerados serán en efectivo.
* El sistema no realizará cálculos fiscales o contables.
* El sistema no realizará automáticamente la venta de los objetos de empeños vencidos.
* El sistema no actualizará automáticamente el estado de pago de un cliente sin que se registre la operación correspondiente.

---

## 2. Usuarios y su contexto

| Usuario      | Qué hace hoy sin el sistema                                                                                                                                                   | Qué espera del sistema                                                                                                                                                           |
| ------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Owner**    | Supervisa los préstamos, pagos, clientes y objetos dejados como garantía. Actualmente la información se registra en libretas o fichas y los cálculos se realizan manualmente. | Consultar la información de los empeños, supervisar las operaciones, conservar un historial de cambios y autorizar operaciones mayores a $50,000.                                |
| **Employee** | Registra clientes, préstamos, objetos y pagos manualmente. También realiza los cálculos de intereses y revisa los adeudos.                                                    | Registrar las operaciones de forma sencilla, consultar la información de los clientes y empeños y obtener los cálculos de intereses y adeudos sin depender de cálculos manuales. |

**Conflictos identificados entre usuarios:**

El Owner necesita tener control sobre la información y evitar que un Employee modifique o elimine datos incorrectamente. Por esta razón, las operaciones mayores a $50,000 requieren autorización del Owner y el sistema debe conservar un historial de modificaciones.

El Employee necesita realizar las operaciones de manera rápida y sencilla, por lo que el sistema debe permitirle registrar y consultar la información necesaria para atender a los clientes sin agregar procesos innecesarios.

---

# 3. Requisitos funcionales

## 3.1 Resumen

| ID     | Nombre                                        | Prioridad      | Origen                           |
| ------ | --------------------------------------------- | -------------- | -------------------------------- |
| RF-001 | Registro de clientes                          | Imprescindible | Visión del producto + entrevista |
| RF-002 | Registro de préstamos y garantías             | Imprescindible | Visión del producto + entrevista |
| RF-003 | Registro de pagos                             | Imprescindible | Visión del producto + entrevista |
| RF-004 | Cálculo de intereses                          | Imprescindible | Entrevista                       |
| RF-005 | Consulta de adeudos y refrendos               | Imprescindible | Visión del producto + entrevista |
| RF-006 | Identificación de empeños vencidos            | Imprescindible | Entrevista                       |
| RF-007 | Autorización de operaciones mayores a $50,000 | Imprescindible | Entrevista                       |
| RF-008 | Historial de modificaciones                   | Importante     | Entrevista                       |

---

## 3.2 Fichas

### RF-001 · Registro de clientes

| Campo                      | Contenido                                                                                                                                                                                                                   |
| -------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Descripción**            | El sistema registra la información necesaria de cada cliente y permite consultarla posteriormente.                                                                                                                          |
| **Origen**                 | Visión del producto + entrevista de elicitación.                                                                                                                                                                            |
| **Prioridad**              | Imprescindible                                                                                                                                                                                                              |
| **Criterio de aceptación** | Al registrar un cliente con los datos requeridos, el sistema guarda la información y permite consultarla posteriormente. Si falta un dato obligatorio, el sistema no permite guardar el registro e indica el dato faltante. |
| **Relacionado con**        | RF-002, RF-003, RF-005, RNF-USA-001, RNF-INT-001                                                                                                                                                                            |

### RF-002 · Registro de préstamos y garantías

| Campo                      | Contenido                                                                                                                                         |
| -------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Descripción**            | El sistema registra un préstamo asociado a un cliente y registra el objeto entregado como garantía del préstamo.                                  |
| **Origen**                 | Visión del producto + entrevista de elicitación.                                                                                                  |
| **Prioridad**              | Imprescindible                                                                                                                                    |
| **Criterio de aceptación** | Al registrar un préstamo con su cliente, monto, fecha y garantía, el sistema guarda la información y la relaciona con el cliente correspondiente. |
| **Relacionado con**        | RF-001, RF-004, RF-005, RF-006, RF-007, RNF-INT-001                                                                                               |

### RF-003 · Registro de pagos

| Campo                      | Contenido                                                                                                                                     |
| -------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------- |
| **Descripción**            | El sistema registra los pagos realizados sobre un empeño, incluyendo la fecha y el monto pagado.                                              |
| **Origen**                 | Visión del producto + entrevista de elicitación.                                                                                              |
| **Prioridad**              | Imprescindible                                                                                                                                |
| **Criterio de aceptación** | Al registrar un pago con fecha y monto válidos, el sistema lo guarda asociado al empeño correspondiente y permite consultarlo posteriormente. |
| **Relacionado con**        | RF-002, RF-004, RF-005, RF-006, RNF-INT-001                                                                                                   |

### RF-004 · Cálculo de intereses

| Campo                      | Contenido                                                                                                                                                                                                                                    |
| -------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Descripción**            | El sistema calcula los intereses de un empeño de acuerdo con la tasa registrada y los días transcurridos desde el último pago.                                                                                                               |
| **Origen**                 | Entrevista de elicitación.                                                                                                                                                                                                                   |
| **Prioridad**              | Imprescindible                                                                                                                                                                                                                               |
| **Criterio de aceptación** | Al consultar un empeño, el sistema calcula los intereses utilizando la tasa registrada y los días transcurridos desde el último pago. El resultado debe corresponder al número de días transcurridos y no asumir un periodo fijo de 30 días. |
| **Relacionado con**        | RF-002, RF-003, RF-005, RF-006, RNF-EXA-001                                                                                                                                                                                                  |

### RF-005 · Consulta de adeudos y refrendos

| Campo                      | Contenido                                                                                                                                     |
| -------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------- |
| **Descripción**            | El sistema permite consultar el adeudo de un empeño y los refrendos registrados.                                                              |
| **Origen**                 | Visión del producto + entrevista de elicitación.                                                                                              |
| **Prioridad**              | Imprescindible                                                                                                                                |
| **Criterio de aceptación** | Al consultar un empeño, el sistema muestra el saldo o adeudo correspondiente y permite identificar los refrendos registrados para ese empeño. |
| **Relacionado con**        | RF-002, RF-003, RF-004, RF-006, RNF-REN-001, RNF-USA-001                                                                                      |

### RF-006 · Identificación de empeños vencidos

| Campo                      | Contenido                                                                                                                                                        |
| -------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Descripción**            | El sistema identifica los empeños que tienen más de tres meses sin registrar un pago.                                                                            |
| **Origen**                 | Entrevista de elicitación.                                                                                                                                       |
| **Prioridad**              | Imprescindible                                                                                                                                                   |
| **Criterio de aceptación** | Cuando un empeño tiene más de tres meses sin un pago registrado, el sistema lo identifica como vencido y permite consultarlo en el registro de empeños vencidos. |
| **Relacionado con**        | RF-003, RF-005, RF-008, RNF-EXA-001                                                                                                                              |

### RF-007 · Autorización de operaciones mayores a $50,000

| Campo                      | Contenido                                                                                                                                                                                                  |
| -------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Descripción**            | El sistema solicita autorización del Owner antes de completar una operación cuyo monto sea mayor a $50,000.                                                                                                |
| **Origen**                 | Entrevista de elicitación.                                                                                                                                                                                 |
| **Prioridad**              | Imprescindible                                                                                                                                                                                             |
| **Criterio de aceptación** | Cuando una operación supera los $50,000, el sistema no permite completarla hasta que el Owner proporcione la autorización correspondiente. Una operación de $50,000 o menos no requiere esta autorización. |
| **Relacionado con**        | RF-002, RNF-SEG-001, RNF-INT-001                                                                                                                                                                           |

### RF-008 · Historial de modificaciones

| Campo                      | Contenido                                                                                                                                                                               |
| -------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Descripción**            | El sistema conserva un historial de las modificaciones realizadas sobre la información registrada.                                                                                      |
| **Origen**                 | Entrevista de elicitación.                                                                                                                                                              |
| **Prioridad**              | Importante                                                                                                                                                                              |
| **Criterio de aceptación** | Cuando un usuario modifica información registrada, el sistema conserva el registro de la modificación indicando al menos el usuario que realizó el cambio y la fecha en que se realizó. |
| **Relacionado con**        | RF-001, RF-002, RF-003, RF-006, RF-007, RNF-INT-001                                                                                                                                     |

---

# 4. Requisitos no funcionales

## 4.1 Resumen

| ID          | Atributo            | Nombre                           | Prioridad      | Origen                       |
| ----------- | ------------------- | -------------------------------- | -------------- | ---------------------------- |
| RNF-REN-001 | Rendimiento         | Tiempo de consulta               | Importante     | Derivado del tipo de sistema |
| RNF-SEG-001 | Seguridad           | Acceso por usuario               | Imprescindible | Entrevista                   |
| RNF-USA-001 | Usabilidad          | Facilidad de registro y consulta | Imprescindible | Entrevista                   |
| RNF-EXA-001 | Exactitud           | Exactitud de cálculos            | Imprescindible | Entrevista                   |
| RNF-INT-001 | Integridad de datos | Conservación de información      | Imprescindible | Entrevista                   |

---

## 4.2 Fichas

### RNF-REN-001 · Tiempo de consulta

| Campo                   | Contenido                                                                                                                         |
| ----------------------- | --------------------------------------------------------------------------------------------------------------------------------- |
| **Atributo de calidad** | Rendimiento                                                                                                                       |
| **Descripción**         | El sistema debe mostrar la información solicitada de clientes, préstamos o empeños en un tiempo máximo de tres segundos.          |
| **Métrica**             | Tiempo transcurrido entre la solicitud de una consulta y la visualización de los resultados, con hasta 500 registros almacenados. |
| **Origen**              | Derivado del tipo de sistema: sistema de información utilizado para consultas durante la operación de la casa de empeño.          |
| **Prioridad**           | Importante                                                                                                                        |
| **Por qué importa**     | Las consultas se realizan durante la atención a los clientes, por lo que una respuesta lenta dificultaría el uso del sistema.     |
| **Afecta a**            | RF-001, RF-002, RF-005, RF-006                                                                                                    |

### RNF-SEG-001 · Acceso por usuario

| Campo                   | Contenido                                                                                                                                       |
| ----------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------- |
| **Atributo de calidad** | Seguridad                                                                                                                                       |
| **Descripción**         | El sistema debe solicitar identificación de usuario antes de permitir el acceso a la información de clientes, préstamos y pagos.                |
| **Métrica**             | 100% de los accesos a información protegida deben requerir una sesión de usuario válida.                                                        |
| **Origen**              | Entrevista de elicitación.                                                                                                                      |
| **Prioridad**           | Imprescindible                                                                                                                                  |
| **Por qué importa**     | La información de los clientes y las operaciones de la casa de empeño debe estar protegida y solo debe ser modificada por usuarios autorizados. |
| **Afecta a**            | RF-001, RF-002, RF-003, RF-007, RF-008                                                                                                          |

### RNF-USA-001 · Facilidad de registro y consulta

| Campo                   | Contenido                                                                                                                                                            |
| ----------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Atributo de calidad** | Usabilidad                                                                                                                                                           |
| **Descripción**         | El sistema debe permitir que el Employee registre y consulte clientes, préstamos y pagos sin necesitar conocimientos técnicos adicionales.                           |
| **Métrica**             | El Employee debe poder completar un registro de cliente, préstamo o pago después de una capacitación inicial de máximo 30 minutos, sin asistencia del desarrollador. |
| **Origen**              | Entrevista de elicitación.                                                                                                                                           |
| **Prioridad**           | Imprescindible                                                                                                                                                       |
| **Por qué importa**     | El Employee realiza las operaciones diariamente y actualmente utiliza registros manuales, por lo que el sistema debe ser sencillo de utilizar.                       |
| **Afecta a**            | RF-001, RF-002, RF-003, RF-005                                                                                                                                       |

### RNF-EXA-001 · Exactitud de cálculos

| Campo                   | Contenido                                                                                                                                               |
| ----------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Atributo de calidad** | Exactitud                                                                                                                                               |
| **Descripción**         | El sistema debe calcular los intereses y adeudos utilizando correctamente la tasa registrada y los días transcurridos desde el último pago.             |
| **Métrica**             | El resultado calculado debe coincidir con el cálculo manual de referencia en el 100% de los casos de prueba establecidos.                               |
| **Origen**              | Entrevista de elicitación.                                                                                                                              |
| **Prioridad**           | Imprescindible                                                                                                                                          |
| **Por qué importa**     | Actualmente los intereses se calculan manualmente y pueden presentarse errores. Un cálculo incorrecto puede afectar directamente el adeudo del cliente. |
| **Afecta a**            | RF-003, RF-004, RF-005, RF-006                                                                                                                          |

### RNF-INT-001 · Conservación de información

| Campo                   | Contenido                                                                                                                                                     |
| ----------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Atributo de calidad** | Integridad de datos                                                                                                                                           |
| **Descripción**         | El sistema debe conservar los registros de clientes, préstamos, garantías y pagos sin permitir que una modificación elimine el historial de cambios asociado. |
| **Métrica**             | El 100% de las modificaciones realizadas sobre registros deben conservar usuario y fecha de modificación en el historial.                                     |
| **Origen**              | Entrevista de elicitación.                                                                                                                                    |
| **Prioridad**           | Imprescindible                                                                                                                                                |
| **Por qué importa**     | El Owner expresó la necesidad de evitar la pérdida o modificación incorrecta de información y poder revisar los cambios realizados por los usuarios.          |
| **Afecta a**            | RF-001, RF-002, RF-003, RF-006, RF-007, RF-008                                                                                                                |

---

# 5. Casos de uso

Los casos de uso se relacionan con los requisitos funcionales que representan las principales operaciones del sistema.

| ID    | Caso de uso                           | Actor principal  | Requisitos relacionados |
| ----- | ------------------------------------- | ---------------- | ----------------------- |
| CU-01 | Registrar cliente                     | Employee         | RF-001                  |
| CU-02 | Registrar préstamo y garantía         | Employee         | RF-002                  |
| CU-03 | Registrar pago                        | Employee         | RF-003                  |
| CU-04 | Consultar intereses y adeudo          | Employee         | RF-004, RF-005          |
| CU-05 | Consultar empeños vencidos            | Owner / Employee | RF-006                  |
| CU-06 | Autorizar operación mayor a $50,000   | Owner            | RF-007                  |
| CU-07 | Consultar historial de modificaciones | Owner            | RF-008                  |

---

# 6. Trazabilidad

| Requisito   | Origen                           | Caso de uso                                 | Elemento del prototipo           |
| ----------- | -------------------------------- | ------------------------------------------- | -------------------------------- |
| RF-001      | Visión del producto + entrevista | CU-01 Registrar cliente                     | Pantalla de clientes             |
| RF-002      | Visión del producto + entrevista | CU-02 Registrar préstamo y garantía         | Pantalla de nuevo empeño         |
| RF-003      | Visión del producto + entrevista | CU-03 Registrar pago                        | Pantalla de pagos                |
| RF-004      | Entrevista                       | CU-04 Consultar intereses y adeudo          | Pantalla de detalle del empeño   |
| RF-005      | Visión del producto + entrevista | CU-04 Consultar intereses y adeudo          | Pantalla de detalle del empeño   |
| RF-006      | Entrevista                       | CU-05 Consultar empeños vencidos            | Pantalla de empeños vencidos     |
| RF-007      | Entrevista                       | CU-06 Autorizar operación mayor a $50,000   | Pantalla de autorización         |
| RF-008      | Entrevista                       | CU-07 Consultar historial de modificaciones | Pantalla de historial            |
| RNF-REN-001 | Tipo de sistema                  | CU-01, CU-02, CU-04, CU-05                  | Pantallas de consulta            |
| RNF-SEG-001 | Entrevista                       | CU-01 a CU-07                               | Pantalla de inicio de sesión     |
| RNF-USA-001 | Entrevista                       | CU-01, CU-02, CU-03, CU-04                  | Interfaz de registro y consulta  |
| RNF-EXA-001 | Entrevista                       | CU-04                                       | Pantalla de cálculo de intereses |
| RNF-INT-001 | Entrevista                       | CU-01, CU-02, CU-03, CU-06, CU-07           | Pantalla de historial            |

---

# 7. Registro de cambios

| Fecha      | Requisito                 | Qué cambió                                                                                                          | Por qué                                                                                               |
| ---------- | ------------------------- | ------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------- |
| 28/09/2026 | RF-001 a RF-008           | Se documentaron los requisitos funcionales con descripción, origen, prioridad, criterio de aceptación y relaciones. | Integrar la información de la Visión del Producto y la entrevista en la especificación de requisitos. |
| 28/09/2026 | RNF-REN-001 a RNF-INT-001 | Se definieron requisitos no funcionales con métricas verificables.                                                  | Cumplir con la guía de redacción y establecer criterios medibles de calidad.                          |
| 28/09/2026 | RF-007                    | Se estableció la autorización del Owner para operaciones mayores a $50,000.                                         | Regla identificada durante la entrevista.                                                             |
| 28/09/2026 | RF-008                    | Se incorporó el historial de modificaciones.                                                                        | Necesidad identificada durante la entrevista para proteger la información y revisar cambios.          |

---

## Revisión antes de entregar

* [x] Todos los requisitos tienen identificador único.
* [x] Cada requisito expresa una sola idea.
* [x] Cada requisito funcional tiene un criterio de aceptación comprobable.
* [x] Cada requisito no funcional tiene una métrica.
* [x] El campo Origen distingue información proveniente de la Visión, entrevista o derivada del tipo de sistema.
* [x] Se incluyeron requisitos de rendimiento, seguridad, usabilidad, exactitud e integridad de datos.
* [x] Los requisitos se mantienen dentro del alcance declarado.
* [x] Se incluyó la tabla de trazabilidad.
* [x] Se incluyó el registro de cambios.
* [x] Se eliminaron los ejemplos de la plantilla.
* [ ] Revisión por la dupla: pendiente de realizar y registrar.
