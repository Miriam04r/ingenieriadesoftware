# Especificación de requisitos

**Sistema:** EmpeñoControl

**Autor:** Miriam Gómez Mariscal

**Fecha última actualización:** 28/09/2026

---

# 1. Propósito y alcance

## Propósito del documento

Este documento define los requisitos del sistema EmpeñoControl, tomando como base la Visión del producto y la información obtenida en la entrevista realizada al Owner de la casa de empeño.

Su propósito es establecer qué debe hacer el sistema, quiénes lo utilizarán, qué características debe tener y qué aspectos quedan fuera del alcance.

## Alcance del sistema

### Dentro del alcance

* Calcula intereses ingresando los datos del cliente.
* Hace un balance de cuánto dinero tiene prestado el Owner y cuánto dinero le está generando.
* Permite hacer un registro manual de cada cliente y empeño con su información correspondiente.
* Subraya a los empeños que están vencidos de color rojo y los manda arriba de la lista manteniendo al más antiguo al principio.
* Mantiene un historial de las modificaciones realizadas en los registros.
* Permite registrar los pagos realizados por los clientes.
* Permite identificar los pagos pendientes y cuánto tiempo lleva un cliente sin pagar.
* Permite distinguir los empeños activos de los inactivos.

### Explícitamente fuera del alcance

* No calcula el impuesto de cada cliente por sí solo, sino que cuando se necesita saber se ingresan los datos y se calcula.
* No manda un aviso de cuando un cliente se atrasó con el pago.
* El estado de los pagos no se actualiza automáticamente.

**Por qué queda fuera:** Esto queda fuera del alcance porque el sistema no puede saber por sí solo si el cliente pagó, ya que los pagos se hacen en efectivo, por eso el empleado tiene que registrar manualmente cada pago en el sistema.

---

# 2. Usuarios y contexto

| Usuario  | Qué hace hoy sin sistema                                                                               | Qué espera del sistema                                                                                            |
| -------- | ------------------------------------------------------------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------- |
| Owner    | Supervisa los préstamos, revisa los pagos, controla el dinero y revisa los empeños activos y vencidos. | Supervisar clientes, préstamos, pagos y ganancias, además de tener control sobre los préstamos mayores a $50,000. |
| Employee | Atiende a los clientes, registra los empeños y recibe los pagos.                                       | Registrar datos, pagos y calcular intereses automáticamente.                                                      |

## Conflictos identificados

El Employee puede querer realizar un préstamo de cualquier cantidad para agilizar la atención al cliente, mientras que el Owner quiere tener mayor control sobre los préstamos de cantidades altas.

Por ello, cuando un préstamo supere los **$50,000 pesos**, se requiere la autorización del Owner antes de completar la operación.

---

# 3. Requisitos funcionales

## 3.1 Resumen

| ID     | Nombre                                                  | Prioridad | Origen                                                                                                                                                                        |
| ------ | ------------------------------------------------------- | --------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| RF-001 | Registrar clientes                                      | Alta      | Visión de producto · Alcance                                                                                                                                                  |
| RF-002 | Registrar préstamos y empeños                           | Alta      | Entrevista · 22 de septiembre de 2026 · “¿Qué información o funciones consideras indispensables que debería tener un sistema para facilitar el control de la casa de empeño?” |
| RF-003 | Registrar pagos                                         | Alta      | Entrevista · 22 de septiembre de 2026 · “¿Cómo registran los pagos que realizan los clientes?”                                                                                |
| RF-004 | Calcular intereses                                      | Alta      | Visión de producto · Alcance                                                                                                                                                  |
| RF-005 | Mostrar pagos pendientes y tiempo sin pagar             | Alta      | Visión de producto · Descripción del sistema                                                                                                                                  |
| RF-006 | Mostrar balance del dinero prestado y generado          | Media     | Visión de producto · Alcance                                                                                                                                                  |
| RF-007 | Identificar y ordenar empeños vencidos                  | Alta      | Visión de producto · Alcance                                                                                                                                                  |
| RF-008 | Mantener historial de modificaciones                    | Alta      | Visión de producto · Alcance                                                                                                                                                  |
| RF-009 | Solicitar autorización para préstamos mayores a $50,000 | Alta      | Visión de producto · Problema y usuarios                                                                                                                                      |
| RF-010 | Conservar la información de clientes, préstamos y pagos | Alta      | Entrevista · 22 de septiembre de 2026 · “¿Qué sucede cuando un cliente deja de regresar y tiene un empeño pendiente?”                                                         |
| RF-011 | Distinguir empeños activos e inactivos                  | Alta      | Entrevista · 22 de septiembre de 2026 · “¿Qué sucede cuando un cliente deja de regresar y tiene un empeño pendiente?”                                                         |

---

## 3.2 Fichas de requisitos

### RF-001 · Registrar clientes

**Descripción:**
El sistema debe permitir registrar la información correspondiente de cada cliente.

**Origen:** Visión de producto · Alcance

**Prioridad:** Alta

**Criterio de aceptación:**
Dado que el usuario está registrando un cliente, cuando ingrese la información correspondiente y guarde el registro, entonces el cliente debe quedar registrado en el sistema.

**Relacionado con:** CU-001 Registrar cliente

---

### RF-002 · Registrar préstamos y empeños

**Descripción:**
El sistema debe permitir registrar los préstamos y los objetos dejados como garantía por los clientes.

**Origen:** Entrevista · 22 de septiembre de 2026 · “¿Qué información o funciones consideras indispensables que debería tener un sistema para facilitar el control de la casa de empeño?”

**Prioridad:** Alta

**Criterio de aceptación:**
Dado que existe un cliente registrado, cuando el usuario registre un préstamo y su empeño correspondiente, entonces la información debe quedar almacenada y relacionada con el cliente.

**Relacionado con:** CU-002 Registrar préstamo y empeño

---

### RF-003 · Registrar pagos

**Descripción:**
El sistema debe permitir registrar manualmente los pagos realizados por los clientes.

**Origen:** Entrevista · 22 de septiembre de 2026 · “¿Cómo registran los pagos que realizan los clientes?”

**Prioridad:** Alta

**Criterio de aceptación:**
Dado que existe un empeño registrado, cuando el usuario registre un pago realizado por el cliente, entonces el pago debe quedar registrado en el sistema.

**Relacionado con:** CU-003 Registrar pago

---

### RF-004 · Calcular intereses

**Descripción:**
El sistema debe calcular los intereses de los empeños de acuerdo con los datos registrados y los días transcurridos.

**Origen:** Visión de producto · Alcance

**Prioridad:** Alta

**Criterio de aceptación:**
Dado un empeño con sus datos registrados, cuando el usuario solicite el cálculo de intereses, entonces el sistema debe mostrar el interés correspondiente de acuerdo con los días transcurridos.

**Relacionado con:** CU-004 Calcular intereses

---

### RF-005 · Mostrar pagos pendientes y tiempo sin pagar

**Descripción:**
El sistema debe mostrar qué clientes tienen pagos pendientes y cuánto tiempo llevan sin pagar.

**Origen:** Visión de producto · Descripción del sistema

**Prioridad:** Alta

**Criterio de aceptación:**
Dado que existen clientes con pagos pendientes, cuando el usuario consulte los empeños, entonces el sistema debe mostrar cuáles tienen pagos pendientes y el tiempo transcurrido desde el último pago.

**Relacionado con:** CU-005 Consultar pagos pendientes

---

### RF-006 · Mostrar balance del dinero prestado y generado

**Descripción:**
El sistema debe mostrar un balance del dinero que tiene prestado el Owner y cuánto dinero le está generando.

**Origen:** Visión de producto · Alcance

**Prioridad:** Media

**Criterio de aceptación:**
Dado que existen préstamos e intereses registrados, cuando el usuario consulte el balance, entonces el sistema debe mostrar el dinero prestado y el dinero generado.

**Relacionado con:** CU-006 Consultar balance

---

### RF-007 · Identificar y ordenar empeños vencidos

**Descripción:**
El sistema debe identificar los empeños vencidos, mostrarlos de color rojo y colocarlos al inicio de la lista, manteniendo primero el empeño vencido más antiguo.

**Origen:** Visión de producto · Alcance

**Prioridad:** Alta

**Criterio de aceptación:**
Dado que existen empeños que llevan más de tres meses sin pagar intereses, cuando el usuario consulte la lista de empeños, entonces estos deben aparecer identificados en rojo y ordenados al inicio de la lista, colocando primero el más antiguo.

**Relacionado con:** CU-007 Consultar empeños vencidos

---

### RF-008 · Mantener historial de modificaciones

**Descripción:**
El sistema debe mantener un historial de las modificaciones realizadas en los registros para poder revisar qué información fue modificada.

**Origen:** Visión de producto · Alcance

**Prioridad:** Alta

**Criterio de aceptación:**
Dado que un usuario modifica un registro, cuando la modificación sea guardada, entonces el sistema debe conservar el registro de la modificación realizada.

**Relacionado con:** CU-008 Consultar historial de modificaciones

---

### RF-009 · Solicitar autorización para préstamos mayores a $50,000

**Descripción:**
El sistema debe requerir la autorización del Owner antes de completar un préstamo mayor a $50,000 pesos.

**Origen:** Visión de producto · Problema y usuarios

**Prioridad:** Alta

**Criterio de aceptación:**
Dado que el Employee intenta registrar un préstamo mayor a $50,000 pesos, cuando intente completar la operación, entonces el sistema debe solicitar la autorización del Owner antes de finalizarla.

**Relacionado con:** CU-009 Autorizar préstamo mayor a $50,000

---

### RF-010 · Conservar la información de clientes, préstamos y pagos

**Descripción:**
El sistema debe conservar la información de los clientes, préstamos y pagos aunque el cliente deje de acudir al negocio.

**Origen:** Entrevista · 22 de septiembre de 2026 · “¿Qué sucede cuando un cliente deja de regresar y tiene un empeño pendiente?”

**Prioridad:** Alta

**Criterio de aceptación:**
Dado que un cliente deja de acudir al negocio, cuando el usuario consulte su información, entonces sus registros anteriores de clientes, préstamos y pagos deben seguir disponibles.

**Relacionado con:** CU-010 Consultar información de cliente

---

### RF-011 · Distinguir empeños activos e inactivos

**Descripción:**
El sistema debe permitir distinguir los empeños activos de los empeños inactivos.

**Origen:** Entrevista · 22 de septiembre de 2026 · “¿Qué sucede cuando un cliente deja de regresar y tiene un empeño pendiente?”

**Prioridad:** Alta

**Criterio de aceptación:**
Dado que un empeño deja de estar activo, cuando se actualice su estado, entonces debe poder identificarse como inactivo y diferenciarse de los empeños activos.

**Relacionado con:** CU-011 Actualizar estado del empeño

---

# 4. Requisitos no funcionales

## 4.1 Resumen

| ID      | Atributo                | Nombre                             | Prioridad | Origen                                    |
| ------- | ----------------------- | ---------------------------------- | --------- | ----------------------------------------- |
| RNF-001 | Exactitud               | Cálculo correcto de intereses      | Alta      | Visión de producto · Atributos de calidad |
| RNF-002 | Seguridad               | Permisos según función             | Alta      | Visión de producto · Atributos de calidad |
| RNF-003 | Integridad de los datos | Información correcta y consistente | Alta      | Visión de producto · Atributos de calidad |

---

## 4.2 Fichas de requisitos

### RNF-001 · Cálculo correcto de intereses

**Atributo de calidad:** Exactitud

**Descripción:**
El sistema debe realizar correctamente los cálculos de intereses de los empeños.

**Métrica:**
En las pruebas realizadas con datos conocidos, el resultado del cálculo debe coincidir con el resultado esperado en el 100% de los casos.

**Origen:** Visión de producto · Atributos de calidad

**Prioridad:** Alta

**Por qué importa:**
Un cálculo incorrecto puede provocar cobros incorrectos, pérdidas de dinero o problemas con los clientes.

**Afecta a:** RF-004

---

### RNF-002 · Permisos según función

**Atributo de calidad:** Seguridad

**Descripción:**
La información de clientes, préstamos, pagos y dinero debe estar protegida y cada usuario debe tener permisos de acuerdo con su función.

**Métrica:**
En las pruebas de permisos, el 100% de las acciones restringidas debe impedir el acceso a usuarios que no tengan autorización.

**Origen:** Visión de producto · Atributos de calidad

**Prioridad:** Alta

**Por qué importa:**
Un empleado podría modificar información que no debería o se podría perder información importante.

**Afecta a:** RF-001, RF-002, RF-003, RF-008 y RF-009

---

### RNF-003 · Información correcta y consistente

**Atributo de calidad:** Integridad de los datos

**Descripción:**
La información de los clientes, préstamos y pagos debe mantenerse correcta y consistente.

**Métrica:**
En las pruebas de integridad, no debe existir ningún registro con información duplicada o inconsistente después de realizar las operaciones de registro y modificación.

**Origen:** Visión de producto · Atributos de calidad

**Prioridad:** Alta

**Por qué importa:**
La información incorrecta podría provocar registros duplicados, diferencias entre el dinero registrado y el dinero real o problemas en el control de los empeños.

**Afecta a:** RF-001, RF-002, RF-003, RF-005, RF-006 y RF-010

---

# 5. Casos de uso

| ID     | Caso de uso                           | Actor principal  | Requisitos relacionados |
| ------ | ------------------------------------- | ---------------- | ----------------------- |
| CU-001 | Registrar cliente                     | Owner / Employee | RF-001                  |
| CU-002 | Registrar préstamo y empeño           | Owner / Employee | RF-002, RF-009          |
| CU-003 | Registrar pago                        | Owner / Employee | RF-003                  |
| CU-004 | Calcular intereses                    | Owner / Employee | RF-004                  |
| CU-005 | Consultar pagos pendientes            | Owner / Employee | RF-005                  |
| CU-006 | Consultar balance                     | Owner            | RF-006                  |
| CU-007 | Consultar empeños vencidos            | Owner / Employee | RF-007, RF-011          |
| CU-008 | Consultar historial de modificaciones | Owner            | RF-008                  |
| CU-009 | Autorizar préstamo mayor a $50,000    | Owner            | RF-009                  |
| CU-010 | Consultar información de cliente      | Owner / Employee | RF-010                  |
| CU-011 | Actualizar estado del empeño          | Owner / Employee | RF-011                  |

---

# 6. Trazabilidad

| Requisito | Origen                                                                                                                                                                        | Caso de uso                                  | Elemento del prototipo              |
| --------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------- | ----------------------------------- |
| RF-001    | Visión de producto · Alcance                                                                                                                                                  | CU-001 Registrar cliente                     | Pantalla de clientes                |
| RF-002    | Entrevista · 22 de septiembre de 2026 · “¿Qué información o funciones consideras indispensables que debería tener un sistema para facilitar el control de la casa de empeño?” | CU-002 Registrar préstamo y empeño           | Pantalla de registro de empeño      |
| RF-003    | Entrevista · 22 de septiembre de 2026 · “¿Cómo registran los pagos que realizan los clientes?”                                                                                | CU-003 Registrar pago                        | Pantalla de pagos                   |
| RF-004    | Visión de producto · Alcance                                                                                                                                                  | CU-004 Calcular intereses                    | Sección de cálculo de intereses     |
| RF-005    | Visión de producto · Descripción del sistema                                                                                                                                  | CU-005 Consultar pagos pendientes            | Lista de empeños y pagos pendientes |
| RF-006    | Visión de producto · Alcance                                                                                                                                                  | CU-006 Consultar balance                     | Pantalla de balance                 |
| RF-007    | Visión de producto · Alcance                                                                                                                                                  | CU-007 Consultar empeños vencidos            | Lista de empeños vencidos           |
| RF-008    | Visión de producto · Alcance                                                                                                                                                  | CU-008 Consultar historial de modificaciones | Pantalla de historial               |
| RF-009    | Visión de producto · Problema y usuarios                                                                                                                                      | CU-009 Autorizar préstamo mayor a $50,000    | Ventana de autorización             |
| RF-010    | Entrevista · 22 de septiembre de 2026 · “¿Qué sucede cuando un cliente deja de regresar y tiene un empeño pendiente?”                                                         | CU-010 Consultar información de cliente      | Historial del cliente               |
| RF-011    | Entrevista · 22 de septiembre de 2026 · “¿Qué sucede cuando un cliente deja de regresar y tiene un empeño pendiente?”                                                         | CU-011 Actualizar estado del empeño          | Estado del empeño                   |

---

# 7. Registro de cambios

| Fecha      | Requisito | Qué cambió                                                              | Por qué                                                           |
| ---------- | --------- | ----------------------------------------------------------------------- | ----------------------------------------------------------------- |
| 28/09/2026 | Todos     | Se creó la especificación de requisitos                                 | Integrar la información de la Visión del producto y la entrevista |
| 28/09/2026 | RF-010    | Se agregó la conservación de información de clientes, préstamos y pagos | Fue identificado durante la entrevista                            |
| 28/09/2026 | RF-011    | Se agregó la distinción entre empeños activos e inactivos               | Fue identificado durante la entrevista                            |

---

## Revisión antes de entregar

* [x] Los requisitos tienen IDs únicos.
* [x] Cada requisito expresa una idea concreta.
* [x] Los requisitos funcionales tienen criterio de aceptación.
* [x] Los requisitos no funcionales tienen una métrica.
* [x] El origen identifica si viene de la Visión o de la entrevista.
* [x] Los atributos de calidad corresponden a los definidos en la Visión.
* [x] No se impone una solución técnica específica.
* [x] Los requisitos están relacionados con el alcance del sistema.
* [x] Se incluyó trazabilidad.
* [x] Se eliminaron las instrucciones y ejemplos de la plantilla.
