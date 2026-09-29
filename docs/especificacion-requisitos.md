# Especificación de requisitos

**Sistema:** EmpeñoControl
**Autor:** Miriam Gómez Mariscal
**Versión:** 1.0
**Fecha de la última actualización:** 28/09/2026

---

## 1. Propósito y alcance

**Propósito del documento:**

Este documento especifica los requisitos funcionales y no funcionales del sistema EmpeñoControl. Está dirigido al Owner, Employee y al equipo encargado del desarrollo del sistema. Su propósito es establecer de forma clara las funciones que debe realizar el sistema y las características de calidad que debe cumplir.

**Alcance del sistema:**

* Calcula intereses ingresando los datos del cliente.
* Hace un balance de cuánto dinero tiene prestado el Owner y cuánto dinero le está generando.
* Permite hacer un registro manual de cada cliente y empeño con su información correspondiente.
* Subraya a los empeños que están vencidos de color rojo y los manda arriba de la lista manteniendo al más antiguo al principio.
* Mantiene un historial de las modificaciones realizadas en los registros.

**Fuera del alcance:**

* No calcula el impuesto de cada cliente por sí solo, sino que cuando se necesita saber se ingresan los datos y se calcula.
* No manda un aviso de cuando un cliente se atrasó con el pago.
* El estado de los pagos no se actualiza automáticamente.

**Por qué queda fuera:**

Esto queda fuera del alcance porque el sistema no puede saber por sí solo si el cliente pagó, ya que los pagos se hacen en efectivo, por eso el Employee tiene que registrar manualmente cada pago en el sistema.

---

## 2. Usuarios y su contexto

| Usuario      | Qué hace hoy sin el sistema                                                                                                                                                                            | Qué espera del sistema                                                                                                                                |
| ------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Owner**    | Supervisa los préstamos, revisa los pagos, las deudas activas y los empeños que ya expiraron. También lleva el control del dinero. Actualmente la información se registra en libretas, hojas y fichas. | Supervisar clientes, préstamos, pagos y ganancias, consultar las deudas y empeños vencidos y tener control sobre las operaciones de cantidades altas. |
| **Employee** | Atiende a los clientes, registra los empeños y recibe los pagos. También puede registrar y administrar los empeños. Actualmente la información se registra manualmente.                                | Registrar datos de clientes, empeños y pagos, y calcular los intereses automáticamente sin que el sistema sea difícil de usar.                        |

**Conflictos identificados entre usuarios:**

El Employee puede querer realizar un préstamo de cualquier cantidad para agilizar la atención al cliente, mientras que el Owner quiere tener mayor control sobre los préstamos de cantidades altas. Por ello, cuando un préstamo supere los $50,000 pesos, el sistema requerirá la autorización del Owner antes de completar la operación.

Además, el Owner se preocupa por perder información o que un error sea irreversible, mientras que el Employee necesita que el sistema sea sencillo de usar y permita registrar los datos de manera práctica.

---

# 3. Requisitos funcionales

## 3.1 Resumen

| ID     | Nombre                                            | Prioridad      | Origen                           |
| ------ | ------------------------------------------------- | -------------- | -------------------------------- |
| RF-001 | Registro de clientes                              | Imprescindible | Visión del producto + entrevista |
| RF-002 | Registro de empeños y objetos como garantía       | Imprescindible | Visión del producto + entrevista |
| RF-003 | Registro de pagos                                 | Imprescindible | Visión del producto + entrevista |
| RF-004 | Cálculo de intereses                              | Imprescindible | Visión del producto + entrevista |
| RF-005 | Balance del dinero prestado y generado            | Importante     | Visión del producto              |
| RF-006 | Consulta de pagos pendientes y tiempo sin pagar   | Imprescindible | Visión del producto + entrevista |
| RF-007 | Identificación y organización de empeños vencidos | Imprescindible | Visión del producto + entrevista |
| RF-008 | Registro de refrendos                             | Importante     | Información del proyecto         |
| RF-009 | Autorización de préstamos mayores a $50,000       | Imprescindible | Visión del producto + entrevista |
| RF-010 | Historial de modificaciones                       | Imprescindible | Visión del producto + entrevista |
| RF-011 | Distinción entre empeños activos e inactivos      | Importante     | Entrevista                       |

---

## 3.2 Fichas

### RF-001 · Registro de clientes

| Campo                      | Contenido                                                                                                                                                                                                                                                                                                                                                          |
| -------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Descripción**            | El sistema permite registrar manualmente la información correspondiente de cada cliente y consultarla posteriormente.                                                                                                                                                                                                                                              |
| **Origen**                 | Visión del producto, sección 3 "Alcance", dentro del alcance: "Permite hacer un registro manual de cada cliente y empeño con su información correspondiente". También confirmado en la entrevista, pregunta "¿Cómo registran actualmente los datos de los clientes y sus empeños?", donde se indicó que actualmente se registra a mano en una libreta y en fichas. |
| **Prioridad**              | Imprescindible                                                                                                                                                                                                                                                                                                                                                     |
| **Criterio de aceptación** | Al registrar un cliente con los datos requeridos, el sistema guarda la información y permite consultarla posteriormente.                                                                                                                                                                                                                                           |
| **Relacionado con**        | RF-002, RF-003, RF-006, RF-010, RNF-INT-001                                                                                                                                                                                                                                                                                                                        |

### RF-002 · Registro de empeños y objetos como garantía

| Campo                      | Contenido                                                                                                                                                                                                                                                                  |
| -------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Descripción**            | El sistema permite registrar cada empeño junto con la información correspondiente del cliente, el préstamo y el objeto dejado como garantía.                                                                                                                               |
| **Origen**                 | Visión del producto, sección 1 "Descripción del sistema", donde se indica que permite registrar clientes, préstamos y objetos dejados como garantía. También confirmado en la entrevista, pregunta "¿Cómo registran actualmente los datos de los clientes y sus empeños?". |
| **Prioridad**              | Imprescindible                                                                                                                                                                                                                                                             |
| **Criterio de aceptación** | Al registrar un empeño con la información correspondiente del cliente, préstamo y objeto como garantía, el sistema guarda la información y permite consultarla posteriormente.                                                                                             |
| **Relacionado con**        | RF-001, RF-003, RF-004, RF-007, RF-009, RF-011, RNF-INT-001                                                                                                                                                                                                                |

### RF-003 · Registro de pagos

| Campo                      | Contenido                                                                                                                                                                                                                                                                                                                                                                              |
| -------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Descripción**            | El sistema permite registrar manualmente los pagos realizados por los clientes sobre sus empeños.                                                                                                                                                                                                                                                                                      |
| **Origen**                 | Visión del producto, sección 3 "Alcance", donde se establece que el estado de los pagos no se actualiza automáticamente. La entrevista, pregunta "¿Cómo registran los pagos que realizan los clientes?", confirmó que los pagos se registran a mano en una libreta. La entrevista también establece que los pagos se realizan en efectivo y el Employee debe registrarlos manualmente. |
| **Prioridad**              | Imprescindible                                                                                                                                                                                                                                                                                                                                                                         |
| **Criterio de aceptación** | Al registrar un pago con la información correspondiente, el sistema lo guarda asociado al empeño correspondiente y permite consultarlo posteriormente.                                                                                                                                                                                                                                 |
| **Relacionado con**        | RF-002, RF-004, RF-006, RF-010, RNF-INT-001                                                                                                                                                                                                                                                                                                                                            |

### RF-004 · Cálculo de intereses

| Campo                      | Contenido                                                                                                                                                                                                                                                                                                                                                                                                                   |
| -------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Descripción**            | El sistema calcula los intereses de un empeño utilizando los datos registrados y considerando proporcionalmente los días transcurridos desde el último pago.                                                                                                                                                                                                                                                                |
| **Origen**                 | Visión del producto, sección 3 "Alcance", donde se establece que el sistema calcula intereses ingresando los datos del cliente. También se relaciona con la regla de negocio 1 de la Visión: "Los intereses se calculan proporcionalmente según los días transcurridos". La entrevista, pregunta "¿Cómo calculan actualmente los intereses de cada empeño?", confirmó que actualmente los cálculos se realizan manualmente. |
| **Prioridad**              | Imprescindible                                                                                                                                                                                                                                                                                                                                                                                                              |
| **Criterio de aceptación** | Al consultar un empeño, el sistema calcula los intereses de acuerdo con los datos registrados y los días transcurridos desde el último pago. El cálculo debe considerar proporcionalmente los días transcurridos.                                                                                                                                                                                                           |
| **Relacionado con**        | RF-003, RF-006, RF-007, RNF-EXA-001                                                                                                                                                                                                                                                                                                                                                                                         |

### RF-005 · Balance del dinero prestado y generado

| Campo                      | Contenido                                                                                                                                                   |
| -------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Descripción**            | El sistema permite consultar un balance de cuánto dinero tiene prestado el Owner y cuánto dinero le está generando.                                         |
| **Origen**                 | Visión del producto, sección 3 "Alcance", dentro del alcance: "Hace un balance de cuanto dinero tiene prestado el owner y cuánto dinero le está generando". |
| **Prioridad**              | Importante                                                                                                                                                  |
| **Criterio de aceptación** | Al consultar el balance, el sistema muestra la cantidad de dinero prestada y la cantidad de dinero generada de acuerdo con la información registrada.       |
| **Relacionado con**        | RF-002, RF-003, RF-004, RNF-EXA-001, RNF-INT-001                                                                                                            |

### RF-006 · Consulta de pagos pendientes y tiempo sin pagar

| Campo                      | Contenido                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| -------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Descripción**            | El sistema permite identificar qué clientes tienen pagos pendientes y cuánto tiempo llevan sin realizar un pago.                                                                                                                                                                                                                                                                                                                                        |
| **Origen**                 | Visión del producto, sección 1 "Descripción del sistema", donde se establece que el sistema mostrará qué clientes tienen pagos pendientes, cuánto tiempo llevan sin pagar y qué empeños ya están vencidos. También confirmado en la entrevista, preguntas "¿Cómo saben actualmente qué clientes tienen pagos pendientes o cuánto tiempo llevan sin pagar?" y "¿Qué es lo que más se les dificulta al llevar el control de los empeños de esta manera?". |
| **Prioridad**              | Imprescindible                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| **Criterio de aceptación** | Al consultar los registros, el sistema permite identificar los clientes que tienen pagos pendientes y muestra cuánto tiempo llevan sin realizar un pago registrado.                                                                                                                                                                                                                                                                                     |
| **Relacionado con**        | RF-003, RF-007, RF-011, RNF-REN-001                                                                                                                                                                                                                                                                                                                                                                                                                     |

### RF-007 · Identificación y organización de empeños vencidos

| Campo                      | Contenido                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| -------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Descripción**            | El sistema identifica los empeños vencidos, los muestra de forma diferenciada y los coloca al inicio de la lista, manteniendo primero al más antiguo.                                                                                                                                                                                                                                                                                                                                 |
| **Origen**                 | Visión del producto, sección 3 "Alcance", donde se establece que los empeños vencidos se subrayan de color rojo y se mandan arriba de la lista manteniendo al más antiguo al principio. También se relaciona con la regla de negocio 2: "El empeño se considera vencido después de tres meses sin pagar interés". La entrevista, pregunta "¿Qué sucede cuando un cliente deja de regresar y tiene un empeño pendiente?", confirmó el tratamiento de los empeños que dejan de pagarse. |
| **Prioridad**              | Imprescindible                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| **Criterio de aceptación** | Cuando un empeño supera tres meses sin pagar intereses, el sistema lo identifica como vencido, lo diferencia visualmente y lo coloca antes que los demás empeños, mostrando primero al que tenga mayor tiempo sin pago.                                                                                                                                                                                                                                                               |
| **Relacionado con**        | RF-003, RF-006, RF-011, RNF-EXA-001                                                                                                                                                                                                                                                                                                                                                                                                                                                   |

### RF-008 · Registro de refrendos

| Campo                      | Contenido                                                                                                                                       |
| -------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------- |
| **Descripción**            | El sistema permite registrar y consultar los refrendos realizados sobre un empeño.                                                              |
| **Origen**                 | Información previamente definida en el proyecto EmpeñoControl sobre el control de refrendos y seguimiento de los empeños.                       |
| **Prioridad**              | Importante                                                                                                                                      |
| **Criterio de aceptación** | Al registrar un refrendo, este queda asociado al empeño correspondiente y puede consultarse posteriormente junto con la información del empeño. |
| **Relacionado con**        | RF-002, RF-003, RF-004, RF-006                                                                                                                  |

### RF-009 · Autorización de préstamos mayores a $50,000

| Campo                      | Contenido                                                                                                                                                                                                                                                                                                                                    |
| -------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Descripción**            | El sistema requiere la autorización del Owner antes de completar un préstamo que supere los $50,000 pesos.                                                                                                                                                                                                                                   |
| **Origen**                 | Visión del producto, sección 2 "Problema y usuarios", apartado "Un conflicto entre usuarios", donde se establece que cuando un préstamo supere los $50,000 pesos el sistema requerirá autorización del Owner. También confirmado en la entrevista, pregunta "¿Qué hacen cuando un empleado necesita registrar un préstamo mayor a $50,000?". |
| **Prioridad**              | Imprescindible                                                                                                                                                                                                                                                                                                                               |
| **Criterio de aceptación** | Cuando un Employee intenta completar un préstamo mayor a $50,000, el sistema no permite finalizar la operación hasta que el Owner la autorice.                                                                                                                                                                                               |
| **Relacionado con**        | RF-002, RNF-SEG-001                                                                                                                                                                                                                                                                                                                          |

### RF-010 · Historial de modificaciones

| Campo                      | Contenido                                                                                                                                                                                                                                                                                                                                                                           |
| -------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Descripción**            | El sistema mantiene un historial de las modificaciones realizadas en los registros.                                                                                                                                                                                                                                                                                                 |
| **Origen**                 | Visión del producto, sección 3 "Alcance", dentro del alcance: "Mantiene un historial de las modificaciones realizadas en los registros". También relacionado con la entrevista, pregunta "¿Qué hacen cuando se registra incorrectamente algún dato de un cliente, préstamo o pago?", donde se indicó que actualmente se revisa la información para encontrar el error y corregirlo. |
| **Prioridad**              | Imprescindible                                                                                                                                                                                                                                                                                                                                                                      |
| **Criterio de aceptación** | Cuando se modifica información de un cliente, préstamo, empeño o pago, el sistema conserva el registro de la modificación para poder identificar qué información fue modificada y revisar el cambio realizado.                                                                                                                                                                      |
| **Relacionado con**        | RF-001, RF-002, RF-003, RF-009, RF-011, RNF-INT-001                                                                                                                                                                                                                                                                                                                                 |

### RF-011 · Distinción entre empeños activos e inactivos

| Campo                      | Contenido                                                                                                                                                                                                                                                                                                                                                  |
| -------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Descripción**            | El sistema permite distinguir entre los empeños que se encuentran activos y los que ya se encuentran inactivos.                                                                                                                                                                                                                                            |
| **Origen**                 | Entrevista de elicitación, pregunta "¿Qué sucede cuando un cliente deja de regresar y tiene un empeño pendiente?", donde se indicó que el empeño se registra como inactivo. También identificado en la Bitácora de Entrevista, apartado "Lo que apareció y no esperábamos", donde se establece que los empeños que ya expiraron se separan de los activos. |
| **Prioridad**              | Importante                                                                                                                                                                                                                                                                                                                                                 |
| **Criterio de aceptación** | Cuando un empeño pasa a estar inactivo, el sistema permite distinguirlo de los empeños activos y consultar su información posteriormente.                                                                                                                                                                                                                  |
| **Relacionado con**        | RF-006, RF-007, RF-010, RNF-INT-001                                                                                                                                                                                                                                                                                                                        |

---

# 4. Requisitos no funcionales

## 4.1 Resumen

| ID          | Atributo                | Nombre                                        | Prioridad      | Origen                           |
| ----------- | ----------------------- | --------------------------------------------- | -------------- | -------------------------------- |
| RNF-EXA-001 | Exactitud               | Exactitud de los cálculos                     | Imprescindible | Visión del producto + entrevista |
| RNF-SEG-001 | Seguridad               | Permisos según función                        | Imprescindible | Visión del producto + entrevista |
| RNF-INT-001 | Integridad de los datos | Conservación y consistencia de la información | Imprescindible | Visión del producto + entrevista |

---

## 4.2 Fichas

### RNF-EXA-001 · Exactitud de los cálculos

| Campo                   | Contenido                                                                                                                                                                                                                                                                                                                                                                                        |
| ----------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Atributo de calidad** | Exactitud                                                                                                                                                                                                                                                                                                                                                                                        |
| **Descripción**         | El sistema debe realizar correctamente los cálculos de intereses de acuerdo con los datos registrados y los días transcurridos.                                                                                                                                                                                                                                                                  |
| **Métrica**             | El resultado del cálculo debe coincidir con el cálculo de referencia en el 100% de los casos de prueba establecidos.                                                                                                                                                                                                                                                                             |
| **Origen**              | Visión del producto, sección 4 "Tipo de sistema y restricciones", apartado "Atributos de calidad que impone", donde se establece que el sistema debe realizar correctamente los cálculos de intereses. También confirmado en la entrevista, preguntas "¿Qué problemas han tenido por hacer los cálculos de intereses manualmente?" y "¿Cómo calculan actualmente los intereses de cada empeño?". |
| **Prioridad**           | Imprescindible                                                                                                                                                                                                                                                                                                                                                                                   |
| **Por qué importa**     | Un error en los cálculos puede provocar que se cobren cantidades incorrectas, generar pérdidas de dinero o causar problemas con los clientes.                                                                                                                                                                                                                                                    |
| **Afecta a**            | RF-004, RF-005, RF-006, RF-007                                                                                                                                                                                                                                                                                                                                                                   |

### RNF-SEG-001 · Permisos según función

| Campo                   | Contenido                                                                                                                                                                                                                                                                                                                                                                                     |
| ----------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Atributo de calidad** | Seguridad                                                                                                                                                                                                                                                                                                                                                                                     |
| **Descripción**         | El sistema debe controlar los permisos de los usuarios de acuerdo con su función de Owner o Employee.                                                                                                                                                                                                                                                                                         |
| **Métrica**             | El 100% de las operaciones que requieran autorización del Owner deben bloquearse hasta que el Owner las autorice.                                                                                                                                                                                                                                                                             |
| **Origen**              | Visión del producto, sección 4 "Tipo de sistema y restricciones", apartado "Atributos de calidad que impone", donde se establece que cada usuario debe tener permisos de acuerdo con su función. También relacionado con el conflicto entre usuarios de la sección 2 y confirmado en la entrevista, pregunta "¿Qué hacen cuando un empleado necesita registrar un préstamo mayor a $50,000?". |
| **Prioridad**           | Imprescindible                                                                                                                                                                                                                                                                                                                                                                                |
| **Por qué importa**     | Un empleado podría modificar información que no debería o realizar una operación de una cantidad alta sin la supervisión del Owner.                                                                                                                                                                                                                                                           |
| **Afecta a**            | RF-002, RF-009, RF-010                                                                                                                                                                                                                                                                                                                                                                        |

### RNF-INT-001 · Conservación y consistencia de la información

| Campo                   | Contenido                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| ----------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Atributo de calidad** | Integridad de los datos                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| **Descripción**         | La información de clientes, préstamos, empeños y pagos debe mantenerse correcta y consistente, conservando los cambios realizados en los registros.                                                                                                                                                                                                                                                                                                                      |
| **Métrica**             | El 100% de los registros modificados deben conservar la información necesaria para identificar el cambio realizado y mantener la consistencia del registro.                                                                                                                                                                                                                                                                                                              |
| **Origen**              | Visión del producto, sección 4 "Tipo de sistema y restricciones", apartado "Atributos de calidad que impone", donde se establece que la información de clientes, préstamos y pagos debe mantenerse correcta y consistente. También confirmado en la entrevista, pregunta "¿Qué hacen cuando se registra incorrectamente algún dato de un cliente, préstamo o pago?" y en la Bitácora de Entrevista, donde se identifica la necesidad de conservar y revisar los cambios. |
| **Prioridad**           | Imprescindible                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| **Por qué importa**     | Una información incorrecta o inconsistente podría generar registros duplicados, diferencias entre el dinero registrado y el dinero real o pérdida de información importante.                                                                                                                                                                                                                                                                                             |
| **Afecta a**            | RF-001, RF-002, RF-003, RF-005, RF-010, RF-011                                                                                                                                                                                                                                                                                                                                                                                                                           |

---

# 5. Casos de uso

Los casos de uso se relacionan con los requisitos funcionales que realiza cada actor.

| ID    | Caso de uso                           | Actor principal  | Requisitos relacionados |
| ----- | ------------------------------------- | ---------------- | ----------------------- |
| CU-01 | Registrar cliente                     | Owner / Employee | RF-001                  |
| CU-02 | Registrar empeño y garantía           | Owner / Employee | RF-002                  |
| CU-03 | Registrar pago                        | Owner / Employee | RF-003                  |
| CU-04 | Calcular intereses                    | Owner / Employee | RF-004                  |
| CU-05 | Consultar balance                     | Owner            | RF-005                  |
| CU-06 | Consultar pagos pendientes            | Owner / Employee | RF-006                  |
| CU-07 | Consultar empeños vencidos            | Owner / Employee | RF-007                  |
| CU-08 | Registrar refrendo                    | Owner / Employee | RF-008                  |
| CU-09 | Autorizar préstamo mayor a $50,000    | Owner            | RF-009                  |
| CU-10 | Consultar historial de modificaciones | Owner            | RF-010                  |
| CU-11 | Consultar empeños activos e inactivos | Owner / Employee | RF-011                  |

---

# 6. Trazabilidad

| Requisito   | Origen                                                                                                                                                 | Caso de uso                                 | Elemento del prototipo                  |
| ----------- | ------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------- | --------------------------------------- |
| RF-001      | Visión del producto, sección 3 + entrevista, pregunta "¿Cómo registran actualmente los datos de los clientes y sus empeños?"                           | CU-01 Registrar cliente                     | Pantalla de clientes                    |
| RF-002      | Visión del producto, sección 1 + entrevista, pregunta "¿Cómo registran actualmente los datos de los clientes y sus empeños?"                           | CU-02 Registrar empeño y garantía           | Pantalla de nuevo empeño                |
| RF-003      | Visión del producto, sección 3 + entrevista, pregunta "¿Cómo registran los pagos que realizan los clientes?"                                           | CU-03 Registrar pago                        | Pantalla de pagos                       |
| RF-004      | Visión del producto, sección 3 y regla de negocio 1 + entrevista, pregunta "¿Cómo calculan actualmente los intereses de cada empeño?"                  | CU-04 Calcular intereses                    | Pantalla de cálculo de intereses        |
| RF-005      | Visión del producto, sección 3 "Dentro del alcance"                                                                                                    | CU-05 Consultar balance                     | Pantalla de balance                     |
| RF-006      | Visión del producto, sección 1 + entrevista, pregunta "¿Cómo saben actualmente qué clientes tienen pagos pendientes o cuánto tiempo llevan sin pagar?" | CU-06 Consultar pagos pendientes            | Pantalla de pagos pendientes            |
| RF-007      | Visión del producto, sección 3 y regla de negocio 2 + entrevista, preguntas sobre pagos pendientes y empeños que dejan de pagarse                      | CU-07 Consultar empeños vencidos            | Pantalla de empeños vencidos            |
| RF-008      | Información previamente definida del proyecto sobre refrendos                                                                                          | CU-08 Registrar refrendo                    | Pantalla de refrendos                   |
| RF-009      | Visión del producto, sección 2 + entrevista, pregunta "¿Qué hacen cuando un empleado necesita registrar un préstamo mayor a $50,000?"                  | CU-09 Autorizar préstamo                    | Pantalla de autorización                |
| RF-010      | Visión del producto, sección 3 + entrevista, pregunta "¿Qué hacen cuando se registra incorrectamente algún dato de un cliente, préstamo o pago?"       | CU-10 Consultar historial                   | Pantalla de historial                   |
| RF-011      | Entrevista, pregunta "¿Qué sucede cuando un cliente deja de regresar y tiene un empeño pendiente?" + Bitácora de Entrevista                            | CU-11 Consultar empeños activos e inactivos | Pantalla de empeños activos e inactivos |
| RNF-EXA-001 | Visión del producto, sección 4 "Atributos de calidad que impone" + entrevista                                                                          | CU-04 Calcular intereses                    | Pantalla de cálculo de intereses        |
| RNF-SEG-001 | Visión del producto, sección 4 + conflicto entre usuarios + entrevista                                                                                 | CU-09 Autorizar préstamo                    | Pantalla de autorización                |
| RNF-INT-001 | Visión del producto, sección 4 + entrevista + Bitácora de Entrevista                                                                                   | CU-01 a CU-11                               | Historial de modificaciones             |

---

# 7. Registro de cambios

| Fecha      | Requisito                 | Qué cambió                                                                                                                     | Por qué                                                                                                                                                        |
| ---------- | ------------------------- | ------------------------------------------------------------------------------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 28/09/2026 | RF-001 a RF-011           | Se documentaron los requisitos funcionales a partir de la Visión del producto y la información obtenida durante la entrevista. | Integrar los requisitos de la Unidad 2 en la especificación de requisitos.                                                                                     |
| 28/09/2026 | RF-005                    | Se agregó el balance del dinero prestado y el dinero generado.                                                                 | Esta función aparece explícitamente dentro del alcance de la Visión del producto.                                                                              |
| 28/09/2026 | RF-007                    | Se especificó que los empeños vencidos deben aparecer diferenciados y ordenados con el más antiguo primero.                    | Esta función está definida explícitamente en el alcance de la Visión del producto.                                                                             |
| 28/09/2026 | RF-009                    | Se especificó la autorización del Owner para préstamos mayores a $50,000.                                                      | Regla identificada en la Visión del producto y confirmada durante la entrevista.                                                                               |
| 28/09/2026 | RF-010                    | Se documentó el historial de modificaciones.                                                                                   | Esta función está dentro del alcance de la Visión del producto y se relaciona con el problema de corregir registros incorrectos identificado en la entrevista. |
| 28/09/2026 | RF-011                    | Se agregó la distinción entre empeños activos e inactivos.                                                                     | Esta necesidad apareció durante la entrevista y quedó registrada en la Bitácora de Entrevista como un hallazgo nuevo.                                          |
| 28/09/2026 | RNF-EXA-001 a RNF-INT-001 | Se documentaron los tres atributos de calidad identificados en la Visión del producto con métricas verificables.               | Cumplir con la sección de requisitos no funcionales de la plantilla.                                                                                           |

---

## Antes de entregar

* [x] Todos los requisitos tienen identificador único y ninguno está repetido.
* [x] Cada requisito expresa una sola idea.
* [x] Cada requisito funcional tiene criterio de aceptación comprobable.
* [x] Cada requisito no funcional tiene una métrica.
* [x] El campo Origen distingue lo confirmado por el cliente de lo que proviene de la Visión del producto.
* [x] Hay un requisito no funcional para cada atributo de calidad identificado en la Visión del producto: exactitud, seguridad e integridad de los datos.
* [x] Ningún requisito impone una solución técnica.
* [x] Todos los requisitos caben dentro del alcance declarado.
* [x] La tabla de trazabilidad está completa.
* [x] El registro de cambios está incluido.
* [x] Los ejemplos de la plantilla fueron eliminados.
* [ ] La dupla revisó el documento y su revisión está registrada.
