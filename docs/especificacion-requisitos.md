# Especificación de requisitos

**Sistema:** EmpeñoControl  

**Autor:** Miriam Gómez Mariscal  

**Fecha de la última actualización:** 28/09/2026

---

## 1. Propósito y alcance

**Propósito del documento:**

Este documento describe los requisitos funcionales y no funcionales del sistema EmpeñoControl, tomando como base la Visión del producto y la información obtenida durante la entrevista de elicitación. Está dirigido al equipo de desarrollo y a los usuarios del sistema, principalmente al Owner y al Employee, para establecer qué debe realizar el sistema y cuáles son sus límites.

**Alcance del sistema:**

- Registrar clientes y su información.
- Registrar préstamos o empeños realizados a los clientes.
- Registrar los objetos entregados como garantía de cada empeño.
- Registrar los pagos realizados por los clientes.
- Calcular los intereses de acuerdo con la tasa correspondiente y los días transcurridos desde el último pago.
- Registrar y consultar refrendos de los empeños.
- Consultar el saldo y adeudo de los empeños.
- Identificar los empeños que llevan más de tres meses sin registrar un pago.
- Consultar los empeños atrasados para facilitar su seguimiento.
- Permitir que el Owner autorice operaciones mayores a $50,000.
- Mantener un registro de los cambios realizados en la información del sistema.

**Fuera del alcance:**

- El sistema no determinará por sí mismo la tasa de interés; esta deberá ser ingresada de acuerdo con las reglas del negocio.
- El sistema no realizará cobros automáticos.
- El sistema no enviará alertas automáticas a los clientes cuando tengan un pago pendiente.
- El sistema no realizará automáticamente la venta de los objetos correspondientes a empeños vencidos.
- El sistema no realizará cálculos fiscales o contables.
- El sistema no realizará pagos mediante tarjetas, transferencias u otros medios electrónicos.
- El sistema no actualizará automáticamente un pago si este no ha sido registrado por el usuario.

---

## 2. Usuarios y su contexto

| Usuario | Qué hace hoy sin el sistema | Qué espera del sistema |
| ------- | --------------------------- | ---------------------- |
| **Owner** | Supervisa los empeños, clientes, pagos y objetos que se encuentran como garantía. La información se lleva principalmente de forma manual y necesita revisar que las operaciones sean correctas. | Tener control de la información de los clientes y empeños, consultar los adeudos y empeños atrasados y autorizar operaciones mayores a $50,000. |
| **Employee** | Registra clientes, préstamos, objetos y pagos de forma manual. También realiza los cálculos de intereses y revisa cuándo un cliente lleva varios meses sin pagar. | Registrar y consultar la información de manera sencilla, obtener los cálculos de intereses y conocer el estado de los empeños sin depender de registros y cálculos manuales. |

**Conflictos identificados entre usuarios:**

1. **Owner vs. Employee:** el Employee necesita realizar las operaciones de manera rápida, mientras que el Owner necesita tener control sobre la información y evitar modificaciones o eliminaciones incorrectas. Por esta razón, las operaciones mayores a $50,000 requieren autorización del Owner y se debe conservar un historial de modificaciones.

2. **Employee vs. exactitud de la información:** el Employee necesita registrar las operaciones rápidamente, pero los errores en los cálculos de intereses o en los registros pueden afectar directamente el adeudo de un cliente. El sistema debe facilitar el registro sin perder la exactitud de la información.

---

# 3. Requisitos funcionales

## 3.1 Resumen

| ID | Nombre | Prioridad | Origen |
| ------ | ------ | --------- | ------ |
| RF-001 | Registro de clientes | Imprescindible | Visión del producto + entrevista |
| RF-002 | Registro de empeños y garantías | Imprescindible | Visión del producto + entrevista |
| RF-003 | Registro de pagos | Imprescindible | Visión del producto + entrevista |
| RF-004 | Cálculo de intereses y refrendos | Imprescindible | Entrevista |
| RF-005 | Consulta e identificación de empeños atrasados | Imprescindible | Visión del producto + entrevista |
| RF-006 | Autorización de operaciones mayores a $50,000 | Imprescindible | Entrevista |
| RF-007 | Historial de modificaciones | Importante | Entrevista |

---

## 3.2 Fichas

### RF-001 · Registro de clientes

| Campo | Contenido |
| -------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Descripción** | El sistema permite registrar la información de los clientes y consultarla posteriormente. |
| **Origen** | Visión del producto + entrevista de elicitación. |
| **Prioridad** | Imprescindible |
| **Criterio de aceptación** | Al registrar un cliente con los datos obligatorios, el sistema guarda la información y permite consultarla posteriormente. Si falta un dato obligatorio, el sistema no permite guardar el registro y señala cuál falta. |
| **Relacionado con** | RF-002, RF-003, RF-005, RNF-USA-001 |

### RF-002 · Registro de empeños y garantías

| Campo | Contenido |
| -------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Descripción** | El sistema permite registrar un empeño asociado a un cliente y registrar el objeto entregado como garantía. |
| **Origen** | Visión del producto + entrevista de elicitación. |
| **Prioridad** | Imprescindible |
| **Criterio de aceptación** | Al registrar un empeño con el cliente, monto, fecha y objeto en garantía, el sistema guarda la información y la relaciona con el cliente correspondiente. Si el monto de la operación es mayor a $50,000, el sistema solicita la autorización del Owner antes de completarla. |
| **Relacionado con** | RF-001, RF-004, RF-005, RF-006, RNF-SEG-001 |

### RF-003 · Registro de pagos

| Campo | Contenido |
| -------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Descripción** | El sistema permite registrar los pagos realizados por un cliente sobre un empeño, incluyendo la fecha y el monto pagado. |
| **Origen** | Visión del producto + entrevista de elicitación. |
| **Prioridad** | Imprescindible |
| **Criterio de aceptación** | Al registrar un pago con una fecha y monto válidos, el sistema lo guarda asociado al empeño correspondiente y permite consultarlo posteriormente. |
| **Relacionado con** | RF-002, RF-004, RF-005, RF-007, RNF-INT-001 |

### RF-004 · Cálculo de intereses y refrendos

| Campo | Contenido |
| -------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Descripción** | El sistema calcula los intereses de un empeño de acuerdo con la tasa registrada y los días transcurridos desde el último pago, y permite registrar los refrendos correspondientes. |
| **Origen** | Entrevista de elicitación. |
| **Prioridad** | Imprescindible |
| **Criterio de aceptación** | Al consultar un empeño, el sistema calcula los intereses considerando la tasa registrada y los días transcurridos desde el último pago. El cálculo debe considerar los días reales transcurridos y no asumir automáticamente un periodo fijo de 30 días. Al registrar un refrendo, este queda asociado al empeño y puede consultarse posteriormente. |
| **Relacionado con** | RF-002, RF-003, RF-005, RNF-EXA-001 |

### RF-005 · Consulta e identificación de empeños atrasados

| Campo | Contenido |
| -------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Descripción** | El sistema permite consultar el saldo y adeudo de los empeños e identificar aquellos que llevan más de tres meses sin registrar un pago. |
| **Origen** | Visión del producto + entrevista de elicitación. |
| **Prioridad** | Imprescindible |
| **Criterio de aceptación** | Al consultar los empeños, el sistema permite identificar cuáles llevan más de tres meses sin un pago registrado. Los empeños atrasados deben poder consultarse junto con la información necesaria para darles seguimiento. |
| **Relacionado con** | RF-003, RF-004, RF-007, RNF-REN-001 |

### RF-006 · Autorización de operaciones mayores a $50,000

| Campo | Contenido |
| -------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Descripción** | El sistema solicita la autorización del Owner antes de completar una operación cuyo monto sea mayor a $50,000. |
| **Origen** | Entrevista de elicitación. |
| **Prioridad** | Imprescindible |
| **Criterio de aceptación** | Cuando una operación supera los $50,000, el sistema no permite completarla hasta que el Owner la autorice. Las operaciones de $50,000 o menos pueden continuar sin esta autorización. |
| **Relacionado con** | RF-002, RNF-SEG-001, RNF-INT-001 |

### RF-007 · Historial de modificaciones

| Campo | Contenido |
| -------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Descripción** | El sistema conserva un historial de las modificaciones realizadas sobre la información registrada. |
| **Origen** | Entrevista de elicitación. |
| **Prioridad** | Importante |
| **Criterio de aceptación** | Cuando un usuario modifica información de un cliente, empeño o pago, el sistema conserva el registro de la modificación indicando al menos el usuario que realizó el cambio y la fecha en que se realizó. |
| **Relacionado con** | RF-001, RF-002, RF-003, RF-006, RNF-INT-001 |

---

# 4. Requisitos no funcionales

## 4.1 Resumen

| ID | Atributo | Nombre | Prioridad | Origen |
| ----------- | ----------- | ------ | --------- | ------ |
| RNF-REN-001 | Rendimiento | Tiempo de consulta de información | Importante | Derivado del tipo de sistema |
| RNF-SEG-001 | Seguridad | Acceso según tipo de usuario | Imprescindible | Entrevista |
| RNF-USA-001 | Usabilidad | Registro sencillo de operaciones | Imprescindible | Entrevista |
| RNF-EXA-001 | Exactitud | Exactitud de los cálculos | Imprescindible | Entrevista |
| RNF-INT-001 | Integridad | Conservación de la información | Imprescindible | Entrevista |

---

## 4.2 Fichas

### RNF-REN-001 · Tiempo de consulta de información

| Campo | Contenido |
| ------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Atributo de calidad** | Rendimiento |
| **Descripción** | La información de un cliente o empeño debe mostrarse en un tiempo máximo de tres segundos después de realizar una consulta. |
| **Métrica** | Tiempo entre la solicitud de la consulta y la visualización completa de la información, medido con hasta 500 registros almacenados. |
| **Origen** | Derivado del tipo de sistema: sistema de información utilizado para registrar y consultar operaciones de manera frecuente. |
| **Prioridad** | Importante |
| **Por qué importa** | La información se consulta durante la atención al cliente. Una consulta lenta puede dificultar el registro y seguimiento de las operaciones. |
| **Afecta a** | RF-001, RF-002, RF-005 |

### RNF-SEG-001 · Acceso según tipo de usuario

| Campo | Contenido |
| ------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Atributo de calidad** | Seguridad |
| **Descripción** | El sistema debe restringir las acciones disponibles de acuerdo con el tipo de usuario. El Owner tendrá acceso a las operaciones de supervisión y autorización, mientras que el Employee tendrá acceso a las operaciones que correspondan a su función. |
| **Métrica** | El 100% de las pruebas de acceso no autorizado deben ser bloqueadas correctamente. |
| **Origen** | Entrevista de elicitación. |
| **Prioridad** | Imprescindible |
| **Por qué importa** | El Owner necesita controlar las operaciones y evitar que un usuario modifique información de manera incorrecta o realice operaciones que requieren autorización. |
| **Afecta a** | RF-001, RF-002, RF-003, RF-006, RF-007 |

### RNF-USA-001 · Registro sencillo de operaciones

| Campo | Contenido |
| ------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Atributo de calidad** | Usabilidad |
| **Descripción** | El Employee debe poder registrar clientes, empeños y pagos mediante una interfaz sencilla y comprensible, sin requerir conocimientos técnicos. |
| **Métrica** | El Employee debe poder completar el registro de un cliente, empeño o pago después de una capacitación inicial de máximo 30 minutos. |
| **Origen** | Entrevista de elicitación. |
| **Prioridad** | Imprescindible |
| **Por qué importa** | El Employee realiza las operaciones diariamente y necesita registrar la información sin que el sistema complique el proceso de atención. |
| **Afecta a** | RF-001, RF-002, RF-003 |

### RNF-EXA-001 · Exactitud de los cálculos

| Campo | Contenido |
| ------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Atributo de calidad** | Exactitud |
| **Descripción** | El sistema debe calcular correctamente los intereses y adeudos utilizando la tasa registrada y los días transcurridos desde el último pago. |
| **Métrica** | El resultado del sistema debe coincidir con el cálculo de referencia en el 100% de los casos de prueba definidos. |
| **Origen** | Entrevista de elicitación. |
| **Prioridad** | Imprescindible |
| **Por qué importa** | Actualmente los intereses pueden calcularse manualmente, lo que puede producir errores en el monto que debe pagar el cliente. |
| **Afecta a** | RF-003, RF-004, RF-005 |

### RNF-INT-001 · Conservación de la información

| Campo | Contenido |
| ------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Atributo de calidad** | Integridad |
| **Descripción** | El sistema debe conservar la información registrada de clientes, empeños, garantías y pagos, incluyendo el historial de modificaciones realizadas. |
| **Métrica** | El 100% de las modificaciones realizadas sobre registros deben conservar como mínimo el usuario que realizó el cambio y la fecha de modificación. |
| **Origen** | Entrevista de elicitación. |
| **Prioridad** | Imprescindible |
| **Por qué importa** | El Owner necesita evitar la pérdida de información y poder revisar los cambios realizados sobre los registros. |
| **Afecta a** | RF-001, RF-002, RF-003, RF-006, RF-007 |

---

# 5. Casos de uso

Los casos de uso se relacionan con los requisitos funcionales que representan las principales operaciones del sistema.

| ID | Caso de uso | Actor principal | Requisitos relacionados |
| --- | --- | --- | --- |
| CU-01 | Registrar cliente | Employee | RF-001 |
| CU-02 | Registrar empeño y garantía | Employee | RF-002, RF-006 |
| CU-03 | Registrar pago | Employee | RF-003 |
| CU-04 | Consultar intereses, refrendos y adeudo | Employee | RF-004, RF-005 |
| CU-05 | Consultar empeños atrasados | Owner / Employee | RF-005 |
| CU-06 | Autorizar operación mayor a $50,000 | Owner | RF-006 |
| CU-07 | Consultar historial de modificaciones | Owner | RF-007 |

---

# 6. Trazabilidad

| Requisito | Origen | Caso de uso | Elemento del prototipo |
| --------- | ----------------- | ------------------------ | ---------------------- |
| RF-001 | Visión del producto + entrevista | CU-01 Registrar cliente | Pantalla de clientes |
| RF-002 | Visión del producto + entrevista | CU-02 Registrar empeño y garantía | Pantalla de nuevo empeño |
| RF-003 | Visión del producto + entrevista | CU-03 Registrar pago | Pantalla de pagos |
| RF-004 | Entrevista | CU-04 Consultar intereses, refrendos y adeudo | Pantalla de detalle del empeño |
| RF-005 | Visión del producto + entrevista | CU-05 Consultar empeños atrasados | Pantalla de empeños atrasados |
| RF-006 | Entrevista | CU-02 Registrar empeño y garantía / CU-06 Autorizar operación | Pantalla de autorización |
| RF-007 | Entrevista | CU-07 Consultar historial de modificaciones | Pantalla de historial |
| RNF-REN-001 | Derivado del tipo de sistema | CU-01, CU-02, CU-04, CU-05 | Pantallas de consulta |
| RNF-SEG-001 | Entrevista | CU-01 a CU-07 | Pantalla de acceso |
| RNF-USA-001 | Entrevista | CU-01, CU-02, CU-03 | Pantallas de registro |
| RNF-EXA-001 | Entrevista | CU-04 | Pantalla de cálculo de intereses |
| RNF-INT-001 | Entrevista | CU-01, CU-02, CU-03, CU-06, CU-07 | Pantalla de historial |

---

# 7. Registro de cambios

| Fecha | Requisito | Qué cambió | Por qué |
| ----- | --------- | ---------- | ------- |
| 28/09/2026 | RF-001 a RF-007 | Se documentaron los requisitos funcionales con descripción, origen, prioridad, criterio de aceptación y relaciones. | Integrar la información de la Visión del Producto y la entrevista en la especificación de requisitos. |
| 28/09/2026 | RNF-REN-001 a RNF-INT-001 | Se definieron los requisitos no funcionales con métricas verificables. | Cumplir con la guía de redacción de requisitos. |
| 28/09/2026 | RF-006 | Se incorporó la autorización del Owner para operaciones mayores a $50,000. | Regla identificada durante la entrevista. |
| 28/09/2026 | RF-007 | Se incorporó el historial de modificaciones de la información. | Necesidad identificada durante la entrevista para evitar modificaciones incorrectas y conservar evidencia de los cambios. |

---

## Antes de entregar

- [x] Todos los requisitos tienen identificador único y ninguno está repetido.
- [x] Cada requisito expresa una sola idea.
- [x] Cada requisito funcional tiene criterio de aceptación comprobable.
- [x] Cada requisito no funcional tiene una métrica.
- [x] El campo Origen distingue lo confirmado por el cliente de lo derivado del tipo de sistema.
- [x] Hay requisitos no funcionales para rendimiento, seguridad, usabilidad, exactitud e integridad.
- [x] Ningún requisito impone una solución técnica específica.
- [x] Todos los requisitos están dentro del alcance declarado.
- [x] La tabla de trazabilidad está incluida.
- [x] El registro de cambios está incluido.
- [x] Los ejemplos de la plantilla fueron eliminados.
- [ ] La dupla revisó el documento y registró su revisión.
