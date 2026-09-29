# Especificación de requisitos

**Sistema:** EmpeñoControl

**Autor:** Miriam Gómez Mariscal

**Fecha de la última actualización:** 29/09/2026

## 1. Propósito y alcance

**Propósito del documento:** 
Especificar los requisitos funcionales y no funcionales para el desarrollo del sistema EmpeñoControl, sirviendo como fuente única de verdad para el diseño, desarrollo y validación del software.

**Alcance del sistema:**
- Calcula intereses ingresando los datos del cliente.
- Hace un balance de cuanto dinero tiene prestado el owner y cuánto dinero le está generando.
- Permite hacer un registro manual de cada cliente y empeño con su información correspondiente.
- Subraya a los empeños que están vencidos de color rojo y los manda arriba de la lista manteniendo al más antiguo al principio.
- Mantiene un historial de las modificaciones realizadas en los registros.

**Fuera del alcance:**
- No calcula el impuesto de cada cliente por si solo, si no que cuando se necesita saber se ingresan los datos y se calcula.
- No manda un aviso de cuando un cliente se atrasó con el pago.
- El estado de los pagos no se actualiza automáticamente.

## 2. Usuarios y su contexto

| Usuario | Qué hace hoy sin el sistema | Qué espera del sistema |
| :--- | :--- | :--- |
| **Owner** | Revisa libretas y anotaciones a mano para identificar empeños activos, pagos realizados y deudas pendientes. Separa manualmente los empeños expirados | Supervisar clientes, préstamos, pagos y ganancias sin temor a perder información. Espera distinguir fácilmente los empeños vencidos de los activos |
| **Employee** | Registra clientes, empeños y recibe pagos de forma manual. Calcula intereses a mano con riesgo de equivocarse | Registrar datos y calcular intereses automáticamente sin que el sistema sea complejo de usar |

**Conflictos identificados entre usuarios:**
El Employee puede querer realizar un préstamo de cualquier cantidad para agilizar la atención al cliente, mientras que el Owner quiere tener mayor control sobre los préstamos de cantidades altas. Por ello, cuando un préstamo supere los $50,000 pesos, el sistema requerirá la autorización del Owner.

## 3. Requisitos funcionales

### 3.1 Resumen

| ID | Nombre | Prioridad | Origen |
| :--- | :--- | :--- | :--- |
| RF-001 | Registro de empeño | Imprescindible | Entrevista confirmada |
| RF-002 | Cálculo de interés | Imprescindible | Entrevista confirmada |
| RF-003 | Bloqueo de préstamo mayor | Imprescindible | Entrevista confirmada |
| RF-004 | Actualización a inactivo | Importante | Entrevista (excepción descubierta) |
| RF-005 | Resaltado de vencidos | Importante | Visión del producto |
| RF-006 | Ordenamiento de vencidos | Importante | Visión del producto |
| RF-007 | Balance de dinero | Importante | Visión del producto |
| RF-008 | Historial de modificaciones | Imprescindible | Visión del producto |

### 3.2 Fichas

**RF-001 · Registro de empeño**
| Campo | Contenido |
| :--- | :--- |
| **Descripción** | El sistema registra un empeño asociándolo con los datos del cliente, el objeto en garantía y el monto del préstamo. |
| **Origen** | Entrevista confirmada, confirmación de proceso actual manual. |
| **Prioridad** | Imprescindible |
| **Criterio de aceptación** | Al ingresar nombre, monto y objeto, el sistema crea un nuevo registro y este aparece inmediatamente en la lista de empeños activos. Si falta algún dato, no permite el guardado. |
| **Relacionado con** | RF-002, RNF-INT-001 |

**RF-002 · Cálculo de interés**
| Campo | Contenido |
| :--- | :--- |
| **Descripción** | El sistema calcula los intereses de un empeño basado en los días exactos transcurridos desde el último pago registrado |
| **Origen** | Entrevista confirmada, dolor principal del usuario |
| **Prioridad** | Imprescindible |
| **Criterio de aceptación** | Al consultar un empeño, el sistema muestra el monto de intereses a cobrar multiplicado por los días pasados desde la fecha de último pago, sin intervención manual. |
| **Relacionado con** | RF-001, RNF-EXA-001 |

**RF-003 · Bloqueo de préstamo mayor**
| Campo | Contenido |
| :--- | :--- |
| **Descripción** | El sistema impide registrar un préstamo superior a $50,000 pesos sin una confirmación de autorización del Owner |
| **Origen** | Entrevista confirmada, regla de negocio explícita |
| **Prioridad** | Imprescindible |
| **Criterio de aceptación** | Si el monto ingresado es $50,001 o superior, el botón de guardar se desactiva hasta que se ingresen las credenciales o el PIN de autorización del Owner. |
| **Relacionado con** | RF-001, RNF-SEG-001 |

**RF-004 · Actualización a inactivo**
| Campo | Contenido |
| :--- | :--- |
| **Descripción** | El sistema asigna el estado inactivo a un empeño cuando transcurren más de tres meses sin un registro de pago de intereses |
| **Origen** | Entrevista, excepción y regla de negocio descubierta |
| **Prioridad** | Importante |
| **Criterio de aceptación** | Al avanzar el reloj del sistema a 3 meses + 1 día desde el último pago, el estado del registro cambia automáticamente de "activo" a "inactivo". |
| **Relacionado con** | RF-005, RF-006 |

**RF-005 · Resaltado de vencidos**
| Campo | Contenido |
| :--- | :--- |
| **Descripción** | El sistema muestra los empeños vencidos con la tipografía subrayada en color rojo en las listas de consulta|
| **Origen** | Documento Visión del producto (alcance) |
| **Prioridad** | Importante |
| **Criterio de aceptación** | Cualquier registro cuyo estado sea vencido se renderiza con formato de texto color rojo y subrayado en la vista de lista principal. |
| **Relacionado con** | RF-004, RF-006 |

**RF-006 · Ordenamiento de vencidos**
| Campo | Contenido |
| :--- | :--- |
| **Descripción** | El sistema ordena la lista de empeños ubicando todos los registros vencidos en la parte superior, ordenados desde el más antiguo al más reciente |
| **Origen** | Documento Visión del producto (alcance) |
| **Prioridad** | Importante |
| **Criterio de aceptación** | Al abrir la pantalla principal, los primeros elementos son siempre los empeños vencidos, siendo el elemento #1 el que tiene más tiempo de vencimiento. |
| **Relacionado con** | RF-004, RF-005 |

**RF-007 · Balance de dinero**
| Campo | Contenido |
| :--- | :--- |
| **Descripción** | El sistema calcula el balance total sumando el dinero que está prestado actualmente y el dinero que ha ingresado por cobro de intereses |
| **Origen** | Documento Visión del producto (alcance) |
| **Prioridad** | Importante |
| **Criterio de aceptación** | En la pantalla de reportes, se visualizan dos campos: "Total Prestado" y "Total Generado", cuyos valores coinciden matemáticamente con la suma de todos los registros en base de datos. |
| **Relacionado con** | RF-001, RF-002 |

**RF-008 · Historial de modificaciones**
| Campo | Contenido |
| :--- | :--- |
| **Descripción** | El sistema registra un historial detallado al existir cualquier modificación en los datos de un cliente, préstamo o pago|
| **Origen** | Entrevista, excepción descubierta (errores de registro) |
| **Prioridad** | Imprescindible |
| **Criterio de aceptación** | Tras editar un dato, se genera un registro inmutable en el historial que contiene la fecha, el usuario que hizo el cambio, el dato anterior y el dato nuevo. |
| **Relacionado con** | RNF-SEG-001 |

## 4. Requisitos no funcionales

### 4.1 Resumen

| ID | Atributo | Nombre | Prioridad | Origen |
| :--- | :--- | :--- | :--- | :--- |
| RNF-EXA-001 | Exactitud | Margen de error en cálculo de interés | Imprescindible | Visión del producto |
| RNF-SEG-001 | Seguridad | Inmutabilidad de historiales | Imprescindible | Visión del producto |
| RNF-INT-001 | Integridad | Retención de registros inactivos | Importante | Entrevista (Excepciones) |

### 4.2 Fichas

**RNF-EXA-001 · Margen de error en cálculo de interés**
| Campo | Contenido |
| :--- | :--- |
| **Atributo de calidad** | Exactitud |
| **Descripción** | El módulo de cálculo de intereses procesa los cobros con una variación permitida de cero centavos respecto a las fórmulas matemáticas del negocio |
| **Métrica** | $0.00 de discrepancia o redondeos no autorizados en los cálculos. |
| **Origen** | Visión del producto (atributo impuesto) y Entrevista confirmada|
| **Prioridad** | Imprescindible |
| **Por qué importa** | Si ocurre un error, el Owner puede perder dinero o el cliente molestarse por un cobro injustificado, afectando directamente la viabilidad del negocio |
| **Afecta a** | RF-002 |

**RNF-SEG-001 · Inmutabilidad de historiales**
| Campo | Contenido |
| :--- | :--- |
| **Atributo de calidad** | Seguridad |
| **Descripción** | El historial de modificaciones del sistema impide la alteración o eliminación de sus registros a cualquier rol de usuario |
| **Métrica** | 0% de permisos de escritura o borrado disponibles sobre las tablas del historial de auditoría, incluso para el Owner. |
| **Origen** | Visión del producto (atributo impuesto por riesgo de manipulación) |
| **Prioridad** | Imprescindible |
| **Por qué importa** | Si no se cumple, un empleado podría modificar información incorrecta sin dejar rastro para ocultar un error, imposibilitando la corrección futura |
| **Afecta a** | RF-008 |

**RNF-INT-001 · Retención de registros inactivos**
| Campo | Contenido |
| :--- | :--- |
| **Atributo de calidad** | Integridad de los datos |
| **Descripción** | El gestor de base de datos retiene permanentemente los registros de los clientes que dejan de regresar al negocio |
| **Métrica** | 100% de persistencia a largo plazo para clientes y empeños con estado "inactivo". No existe borrado en cascada. |
| **Origen** | Entrevista (Reglas que conoces) |
| **Prioridad** | Importante |
| **Por qué importa** | El seguimiento de empeños vencidos y artículos que pasan a venta depende directamente de saber a quién pertenecían y cuánto debía|
| **Afecta a** | RF-001, RF-004 |

## 5. Casos de uso

- CU-01 Registrar cliente y empeño
- CU-02 Calcular y registrar pago de interés
- CU-03 Autorizar préstamo superior al límite
- CU-04 Consultar balance financiero
- CU-05 Consultar empeños vencidos y estado de adeudos

## 6. Trazabilidad

| Requisito | Origen | Caso de uso | Elemento del prototipo |
| :--- | :--- | :--- | :--- |
| RF-001 | Entrevista / Visión del producto | CU-01 Registrar cliente y empeño | Pantalla de nuevo empeño |
| RF-002 | Entrevista | CU-02 Calcular y registrar pago | Modal de cobro de intereses |
| RF-003 | Entrevista / Visión del producto | CU-03 Autorizar préstamo superior | Modal de credenciales (Owner) |
| RF-004 | Entrevista | CU-05 Consultar empeños vencidos | Proceso en segundo plano |
| RF-005 | Visión del producto | CU-05 Consultar empeños vencidos | Lista principal de empeños |
| RF-006 | Visión del producto | CU-05 Consultar empeños vencidos | Lista principal de empeños |
| RF-007 | Visión del producto | CU-04 Consultar balance financiero | Pantalla de balance / Dashboard |
| RF-008 | Entrevista / Visión del producto | CU-01, CU-02 | Pantalla de historial de modificaciones |

## 7. Registro de cambios

| Fecha | Requisito | Qué cambió | Por qué |
| :--- | :--- | :--- | :--- |
| 29/09/2026 | Todos | Creación inicial | Documentación inicial de requisitos según elicitación y Visión del Producto. |
