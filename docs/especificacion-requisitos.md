# Especificación de requisitos

**Sistema:** EmpeñoControl  
**Autor:** Miriam Gómez Mariscal    
**Fecha de la última actualización:** 29/09/2026

---

## 1. Propósito y alcance

**Propósito del documento:** Este documento define los requisitos del sistema EmpeñoControl, tomando como base la Visión del producto y la información obtenida en la entrevista realizada al Owner de la casa de empeño. Su propósito es establecer qué debe hacer el sistema, quiénes lo utilizarán, qué características debe tener y qué aspectos quedan fuera del alcance.

**Alcance del sistema:**

- Calcula intereses ingresando los datos del cliente
- Hace un balance de cuanto dinero tiene prestado el owner y cuánto dinero le está generando
- Permite hacer un registro manual de cada cliente y empeño con su información correspondiente
- Subraya a los empeños que están vencidos de color rojo y los manda arriba de la lista manteniendo al más antiguo al principio
- Mantiene un historial de las modificaciones realizadas en los registros

**Fuera del alcance:**

- No calcula el interés de cada cliente por si solo, si no que cuando se necesita saber se ingresan los datos y se calcula
- No manda un aviso de cuando un cliente se atrasó con el pago
- El estado de los pagos no se actualiza automáticamente

**Por qué queda fuera:** Esto queda fuera del alcance porque el sistema no puede saber por sí solo si el cliente pagó, ya que los pagos se hacen en efectivo, por eso el empleado tiene que registrar manualmente cada pago en el sistema.

---

## 2. Usuarios y su contexto

| Usuario  | Qué hace hoy sin el sistema | Qué espera del sistema |
| -------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Owner    | Administra la casa de empeño desde hace varios años. Cada mañana revisa los empeños activos, los pagos realizados, las deudas activas y si algún empeño ya expiró para separarlo. Atiende clientes según lo que necesiten y puede registrar empeños. Lleva todo a mano en libretas y fichas, y calcula los intereses manualmente. Para saber qué clientes tienen pagos pendientes y cuánto tiempo llevan sin pagar, revisa los registros de las libretas. | Supervisar clientes, préstamos, pagos y ganancias. Contar con un registro de préstamos, empeños y clientes, y que los intereses se calculen automáticamente. Le preocupa perder información o que un error sea irreversible. |
| Employee | Atiende a los clientes, registra los empeños y recibe los pagos en efectivo, anotándolos a mano en una libreta y en fichas. | Registrar datos y calcular intereses automáticamente. Le preocupa que el sistema sea difícil de usar o registrar datos incorrectos. |

**Cambios a partir de la revisión de la dupla**

- El registro y la administración de los empeños los pueden realizar tanto el Owner como el Employee, no solo el Owner.
- Cuando un cliente deja de regresar, su empeño no queda simplemente como pendiente: se registra como inactivo y se pone a la venta. Esto cierra uno de los huecos de la Visión.
- Cuando se registra incorrectamente un dato, hoy se revisa toda la información del préstamo para encontrar el error. Esto cierra el otro hueco de la Visión y confirma la necesidad del historial de modificaciones.
- El seguimiento de deudas y empeños vencidos es una tarea diaria del Owner, por lo que el control de estos datos es más importante de lo que se había considerado.

**Conflictos identificados entre usuarios:** El Employee puede querer realizar un préstamo de cualquier cantidad para agilizar la atención al cliente, mientras que el Owner quiere tener mayor control sobre los préstamos de cantidades altas. Por ello, cuando un préstamo supere los $50,000 pesos, el sistema requerirá la autorización del Owner antes de completar la operación.

---

## 3. Requisitos funcionales

### 3.1 Resumen

| ID         | Nombre                                        | Prioridad      | Origen                                                                |
| ---------- | --------------------------------------------- | -------------- | --------------------------------------------------------------------- |
| RF-001     | Registro de cliente                           | Imprescindible | Visión (alcance); entrevista del 22 de septiembre                     |
| RF-002     | Registro de empeño                            | Imprescindible | Visión (alcance); entrevista del 22 de septiembre                     |
| RF-003     | Empeños activos simultáneos por cliente       | Imprescindible | Visión (reglas de negocio); entrevista del 22 de septiembre           |
| RF-004     | Registro manual de pago de interés            | Imprescindible | Visión (fuera del alcance); entrevista del 22 de septiembre           |
| RF-005     | Cálculo de interés                            | Imprescindible | Visión (alcance y reglas de negocio); entrevista del 22 de septiembre |
| RF-006     | Autorización de préstamos mayores a $50,000   | Imprescindible | Visión (conflicto entre usuarios); entrevista del 22 de septiembre    |
| RF-007     | Señalización de empeños vencidos                   | Imprescindible | Visión (alcance y reglas de negocio); entrevista del 22 de septiembre |
| RF-008     | Balance de dinero prestado                    | Importante     | Visión (alcance)                                                      |
| RF-009    | Balance de dinero generado                    | Importante     | Visión (alcance)                                                      |
| RF-010    | Historial de modificaciones                   | Imprescindible | Visión (alcance); entrevista del 22 de septiembre                     |
| RF-011 | Clasificación de estado de los empeños | Importante | Entrevista del 22 de septiembre                                  |

### 3.2 Fichas

#### RF-001 · Registro de cliente

| Campo                  | Contenido                                                                                                                                                                               |
| ---------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Descripción            | El sistema registra un cliente con su nombre completo, teléfono, dirección y número de identificación oficial.                                                                                                       |
| Origen                 | Visión del producto (alcance: registro manual de cada cliente); entrevista del 22 de septiembre, sección Proceso actual.                                                                |
| Prioridad              | Imprescindible                                                                                                                                                                          |
| Criterio de aceptación | Al guardar un cliente, este aparece en la lista de clientes con los datos capturados. Si falta alguno de los datos, el sistema no guarda y señala cuál falta. |
| Relacionado con        | RF-002, RF-003, RNF-CON-003                                                                                                                                                             |

#### RF-002 · Registro de empeño

| Campo                  | Contenido                                                                                                                                                                   |
| ---------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Descripción            | El sistema registra un empeño con el cliente, la descripción del objeto dejado como garantía, el monto del préstamo, la tasa de interés y la fecha del empeño.          |
| Origen                 | Visión del producto (alcance: registro manual de cada empeño); entrevista del 22 de septiembre, sección Proceso actual.                                                     |
| Prioridad              | Imprescindible                                                                                                                                                              |
| Criterio de aceptación | Al guardar un empeño con los cinco datos, este aparece como activo en la lista de empeños con la fecha correcta. Si falta alguno, el sistema no guarda y señala cuál falta. |
| Relacionado con        | RF-001, RF-003, RF-005, RF-006                                                                                                                                              |

#### RF-003 · Empeños activos simultáneos por cliente

| Campo                  | Contenido                                                                                                                                              |
| ---------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Descripción            | El sistema registra más de un empeño activo al mismo tiempo para un mismo cliente.                                                                     |
| Origen                 | Visión del producto (regla de negocio 3); ficha de dominio del guion de entrevista del 22 de septiembre.                                               |
| Prioridad              | Imprescindible                                                                                                                                         |
| Criterio de aceptación | Al registrar dos empeños para el mismo cliente sin cerrar el primero, ambos aparecen como activos y cada uno conserva su propia fecha, monto y estado. |
| Relacionado con        | RF-001, RF-002, RF-007                                                                                                                                 |

#### RF-004 · Registro manual de pago de interés

| Campo                  | Contenido                                                                                                                                                                                                                                                  |
| ---------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Descripción            | El sistema registra un pago de interés de un empeño con fecha y monto, a partir de los datos que captura un usuario.                                                                                                                                       |
| Origen                 | Visión del producto (fuera del alcance: los pagos son en efectivo y el empleado los registra manualmente); entrevista del 22 de septiembre, sección Proceso actual.                                                                                        |
| Prioridad              | Imprescindible                                                                                                                                                                                                                                             |
| Criterio de aceptación | Al registrar un pago con fecha y monto, este aparece en el historial de pagos del empeño y la fecha del último pago se actualiza. Si el pago no se registra, el sistema mantiene la fecha del último pago anterior y el tiempo sin pagar sigue aumentando. |
| Relacionado con        | RF-005, RF-007, RF-009, RF-011, RNF-CON-002                                                                                                                                                                                                                |

#### RF-005 · Cálculo de interés

| Campo                  | Contenido                                                                                                                                                                                                   |
| ---------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Descripción            | El sistema calcula el interés de un empeño de forma proporcional a los días transcurridos desde el último pago.                                                                                             |
| Origen                 | Visión del producto (alcance y regla de negocio 1); entrevista del 22 de septiembre, sección Proceso actual y ficha de dominio.                                                                             |
| Prioridad              | Imprescindible                                                                                                                                                                                              |
| Criterio de aceptación | Para un mismo empeño, el interés calculado a 30 días es el doble del calculado a 15 días. Al ingresar los datos del empeño, el sistema muestra el interés sin que el usuario realice ningún cálculo manual. |
| Relacionado con        | RF-002, RF-004, RF-011, RNF-CON-001                                                                                                                                                                         |

#### RF-006 · Autorización de préstamos mayores a $50,000

| Campo                  | Contenido                                                                                                                                                                                                              |
| ---------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Descripción            | El sistema impide completar un préstamo mayor a $50,000 pesos hasta que el Owner lo autorice.                                                                                                                          |
| Origen                 | Visión del producto (conflicto entre usuarios); entrevista del 22 de septiembre, sección Excepciones.                                                                                                                  |
| Prioridad              | Imprescindible                                                                                                                                                                                                         |
| Criterio de aceptación | Al registrar un préstamo de $50,001, el sistema no lo completa y lo deja pendiente de autorización; cuando el Owner lo autoriza, el préstamo se completa. Un préstamo de $50,000 o menos se completa sin autorización. |
| Relacionado con        | RF-002, RNF-SEG-001                                                                                                                                                                                                    |

#### RF-007 · Señalización de empeños vencidos

| Campo                  | Contenido                                                                                                                                                                 |
| ---------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Descripción            | El sistema marca en rojo un empeño cuando han pasado más de tres meses desde su último pago de interés (o desde su fecha de empeño, si nunca ha tenido un pago) y los manda al principio de la lista.      |
| Origen                 | Visión del producto (alcance y regla de negocio 2); entrevista del 22 de septiembre, sección Dolores y ficha de dominio.                                                  |
| Prioridad              | Imprescindible                                                                                                                                                            |
| Criterio de aceptación | Si el último pago fue el 15 de mayo, el 15 de agosto el empeño no aparece en rojo y el 16 de agosto sí. Si no se registra ningún pago nuevo, el empeño permanece en rojo. |
| Relacionado con        | RF-004, RF-008, RF-009, RF-014                                                                                                                                            |
#### RF-008 · Balance de dinero prestado

| Campo                  | Contenido                                                                                          |
| ---------------------- | -------------------------------------------------------------------------------------------------- |
| Descripción            | El sistema muestra la suma del dinero prestado en los empeños activos.                             |
| Origen                 | Visión del producto (alcance).                                                                     |
| Prioridad              | Importante                                                                                         |
| Criterio de aceptación | Con tres empeños activos de $1,000, $2,000 y $3,000, el balance muestra $6,000 de dinero prestado. |
| Relacionado con        | RF-002, RF-015, RNF-CON-002                                                                        |

#### RF-009 · Balance de dinero generado

| Campo                  | Contenido                                                                                             |
| ---------------------- | ----------------------------------------------------------------------------------------------------- |
| Descripción            | El sistema muestra la suma del dinero generado por los intereses pagados.                             |
| Origen                 | Visión del producto (alcance).                                                                        |
| Prioridad              | Importante                                                                                            |
| Criterio de aceptación | Después de registrar dos pagos de interés de $100 y $150, el balance muestra $250 de dinero generado. |
| Relacionado con        | RF-004, RF-005, RNF-CON-001, RNF-CON-002                                                              |

#### RF-010 · Historial de modificaciones

| Campo                  | Contenido                                                                                                                                                   |
| ---------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Descripción            | El sistema registra cada modificación hecha a un cliente, préstamo o pago con el valor anterior, el valor nuevo, la fecha y el usuario que la realizó.  |
| Origen                 | Visión del producto (alcance); entrevista del 22 de septiembre, sección Excepciones.                                                                        |
| Prioridad              | Imprescindible                                                                                                                                              |
| Criterio de aceptación | Al cambiar el monto de un pago de $500 a $600, el historial muestra una entrada con $500 como valor anterior, $600 como valor nuevo, la fecha y el usuario. |
| Relacionado con        | RF-013, RNF-SEG-002                                                                                                                                         |

#### **RF-011 · Clasificación de estado de los empeños**

| Campo                  | Contenido                                                                                                                                         |
| ---------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| Descripción            | El sistema permite marcar un empeño como inactivo cuando se vence y vendido cuando es comprado por alguien más                                             |
| Origen                 | Entrevista del 22 de septiembre, sección Excepciones.                                                                                        |
| Prioridad              | Importante                                                                                                                                   |
| Criterio de aceptación | Al marcar un empeño como inactivo o vendido, el sistema actualiza correctamente su estado en la lista de empeños. |
| Relacionado con        | RF-007, RF-015, RNF-CON-003                                                                                                                   |

---

## 4. Requisitos no funcionales

### 4.1 Resumen

| ID              | Atributo                       | Nombre                                     | Prioridad      | Origen                                                                                    |
| --------------- | ------------------------------ | ------------------------------------------ | -------------- | ----------------------------------------------------------------------------------------- |
| RNF-CON-001     | Exactitud     | Exactitud del cálculo de interés           | Imprescindible | Visión (atributos de calidad); entrevista del 22 de septiembre                            |
| RNF-CON-002     | Integridad     | Consistencia de los balances               | Imprescindible | Visión (atributos de calidad)                                                             |
| RNF-CON-003 | Integridad| Conservación de registros              | Importante | Entrevista del 22 de septiembre (ficha de dominio)                                  |
| RNF-SEG-001     | Seguridad                      | Permisos por rol                           | Imprescindible | Visión (atributos de calidad y conflicto entre usuarios); entrevista del 22 de septiembre |
| RNF-SEG-002     | Seguridad                      | Inalterabilidad del historial              | Imprescindible | Visión (atributos de calidad y usuarios)                                                  |
| RNF-USA-001 | Usabilidad                | Facilidad de registro para el Employee | Importante | Visión (usuarios)                                                                     |

### 4.2 Fichas

#### RNF-CON-001 · Exactitud del cálculo de interés

| Campo               | Contenido                                                                                                                                                                                                                    |
| ------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Atributo de calidad | Confiabilidad (exactitud)                                                                                                                                                                                                    |
| Descripción         | El sistema calcula el interés de cada empeño con una diferencia de $0.00 pesos respecto al cálculo de verificación.                                                                                                          |
| Métrica             | Diferencia en pesos entre el interés calculado por el sistema y el cálculo de verificación hecho a mano, medida en 20 empeños de prueba con distinto número de días transcurridos. El valor esperado es $0.00 en los 20. |
| Origen              | Visión del producto (atributo Exactitud); entrevista del 22 de septiembre, sección Dolores (errores en los cálculos manuales). La métrica es supuesto propio.                                                            |
| Prioridad           | Imprescindible                                                                                                                                                                                                               |
| Por qué importa     | Si el cálculo es incorrecto, se podrían cobrar cantidades incorrectas y generar pérdidas de dinero o problemas con los clientes.                                                                                             |
| Afecta a            | RF-005, RF-011                                                                                                                                                                                                               |

#### RNF-CON-002 · Consistencia de los balances

| Campo                  | Contenido                                                                                                                                                                                               |
| ---------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Atributo de calidad    | Integridad                                                                                                                                                                 |
| Descripción            | El dinero prestado y el dinero generado que muestra el sistema coinciden con la suma de los préstamos y pagos registrados.                                                                              |
| Métrica                | Diferencia en pesos entre cada balance mostrado y la suma calculada a mano de los registros, después de 20 operaciones de prueba entre registros, pagos y correcciones. El valor esperado es $0.00. |
| Origen                 | Visión del producto (atributo Integridad de los datos). **La métrica es supuesto propio.**                                                                                                              |
| Prioridad              | Imprescindible                                                                                                                                                                                          |
| Por qué importa        | Si los balances no coinciden con los registros, habría diferencias entre el dinero registrado y el dinero real.                                                                                         |
| Afecta a               | RF-004, RF-010, RF-011, RF-013                                                                                                                                                                          |

#### **RNF-CON-003 · Conservación de registros**

| Campo                  | Contenido                                                                                                                                                                                          |
| ---------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Atributo de calidad    | Integridad                                                                                                                                                        |
| Descripción            | El sistema conserva los registros de clientes, préstamos y pagos aunque el cliente deje de acudir al negocio.                                                                                 |
| Métrica                | Porcentaje de registros de un cliente que siguen consultables después de simular 12 meses sin actividad de ese cliente. El valor esperado es 100%, con 0 registros eliminados automáticamente. |
| Origen                 | Guion de entrevista del 22 de septiembre, ficha de dominio (regla de conservación de información). La métrica es supuesto propio.                                                              |
| Prioridad              | Importante                                                                                                                                                                                     |
| Por qué importa        | Si se pierden los registros de un cliente que dejó de acudir, se pierde el respaldo de sus préstamos y pagos anteriores.                                                                   |
| Afecta a               | RF-001, RF-002, RF-004, RF-014                                                                                                                                                                 |

#### RNF-SEG-001 · Permisos por rol

| Campo                  | Contenido                                                                                                                                                                               |
| ---------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Atributo de calidad    | Seguridad                                                                                                                                                                               |
| Descripción            | El sistema restringe las funciones reservadas al Owner para que el Employee no pueda ejecutarlas.                                                                                       |
| Métrica                | Porcentaje de intentos de un usuario con rol Employee por autorizar un préstamo mayor a $50,000 que el sistema rechaza, medido en 10 intentos de prueba. El valor esperado es 100%. |
| Origen                 | Visión del producto (atributo Seguridad y conflicto entre usuarios); entrevista del 22 de septiembre, sección Excepciones. La métrica es supuesto propio.                           |
| Prioridad              | Imprescindible                                                                                                                                                                          |
| Por qué importa        | Si un empleado pudiera ejecutar funciones del Owner, podría modificar información o autorizar préstamos que no debería.                                                                 |
| Afecta a               | RF-006                                                                                                                                                                                  |

#### RNF-SEG-002 · Inalterabilidad del historial

| Campo                  | Contenido                                                                                                                                                     |
| ---------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Atributo de calidad    | Seguridad                                                                                                                                                     |
| Descripción            | Ningún usuario puede modificar ni eliminar las entradas del historial de modificaciones.                                                                      |
| Métrica                | Número de intentos exitosos de modificar o eliminar una entrada del historial, medido en 10 intentos de prueba con cada rol. El valor esperado es 0.      |
| Origen                 | Visión del producto (atributo Seguridad y preocupación del Owner de que un error sea irreversible). La métrica es supuesto propio.                        |
| Prioridad              | Imprescindible                                                                                                                                                |
| Por qué importa        | Si el historial se pudiera alterar, un error o una modificación indebida podría quedar sin rastro y no se podría corregir sin perder la información anterior. |
| Afecta a               | RF-012, RF-013                                                                                                                                                |

#### **RNF-USA-001 · Facilidad de registro para el Employee**

| Campo                  | Contenido                                                                                                                                                                        |
| ---------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Atributo de calidad    | Usabilidad                                                                                                                                                                 |
| Descripción            | Un Employee sin capacitación previa registra un cliente nuevo y su empeño en menos de cinco minutos.                                                                        |
| Métrica                | Tiempo entre abrir el registro de cliente y guardar su empeño, medido en la primera prueba de cada Employee sin capacitación previa. El valor esperado es menor a 5 minutos. |
| Origen                 | Visión del producto (preocupación del Employee: que sea difícil de usar). La métrica es supuesto propio.                                                                     |
| Prioridad              | Importante                                                                                                                                                                   |
| Por qué importa        | Si el sistema es difícil de usar, el Employee puede registrar datos incorrectos o volver a las libretas.                                                                    |
| Afecta a               | RF-001, RF-002                                                                                                                                                              |

---

## 5. Casos de uso

### CU-01 · Registrar un cliente

| **Campo** | **Contenido** |
|---|---|
| **Actor principal** | Owner / Employee |
| **Objetivo** | Registrar los datos de un nuevo cliente para poder asociarlo con sus empeños y préstamos. |
| **Precondición** | El usuario ha iniciado sesión en el sistema. |
| **Escenario principal** | 1. El usuario selecciona la opción para registrar un cliente.<br>2. El sistema muestra el formulario de registro.<br>3. El usuario ingresa el nombre completo, teléfono, dirección y número de identificación oficial.<br>4. El sistema verifica que los datos requeridos estén completos.<br>5. El sistema registra al cliente y lo muestra en la lista de clientes. |
| **Flujos alternos** | 4a. Falta algún dato: el sistema señala el dato que falta y no permite guardar el registro hasta completarlo. |
| **Postcondición** | El cliente queda registrado y disponible para asociarlo con un empeño. |
| **Requisitos que realiza** | RF-001, RNF-USA-001, RNF-CON-003 |


### CU-02 · Registrar un empeño

| **Campo** | **Contenido** |
|---|---|
| **Actor principal** | Owner / Employee |
| **Objetivo** | Registrar un empeño relacionándolo con un cliente, un objeto como garantía y un préstamo. |
| **Precondición** | El cliente ya está registrado en el sistema. |
| **Escenario principal** | 1. El usuario busca y selecciona al cliente.<br>2. El sistema muestra los datos del cliente.<br>3. El usuario ingresa la descripción del objeto, el monto del préstamo, la tasa de interés y la fecha del empeño.<br>4. El sistema verifica que los datos requeridos estén completos.<br>5. El sistema registra el empeño como activo.<br>6. El sistema muestra el empeño en la lista correspondiente. |
| **Flujos alternos** | 3a. El cliente ya tiene otro empeño activo: el sistema permite registrar el nuevo empeño sin cerrar el anterior.<br><br>4a. El préstamo es mayor a $50,000: el sistema deja el préstamo pendiente de autorización del Owner antes de completarlo. |
| **Postcondición** | El empeño queda registrado y asociado al cliente. Si el préstamo supera los $50,000, queda pendiente de autorización. |
| **Requisitos que realiza** | RF-002, RF-003, RF-006, RNF-USA-001, RNF-CON-003 |


### CU-03 · Registrar un pago de interés

| **Campo** | **Contenido** |
|---|---|
| **Actor principal** | Owner / Employee |
| **Objetivo** | Registrar manualmente el pago de interés realizado por un cliente y actualizar la información del empeño. |
| **Precondición** | El cliente y su empeño ya están registrados en el sistema. |
| **Escenario principal** | 1. El usuario busca y selecciona el empeño del cliente.<br>2. El sistema muestra la información del empeño y la fecha del último pago.<br>3. El usuario ingresa la fecha y el monto del pago recibido.<br>4. El sistema registra el pago.<br>5. El sistema actualiza la fecha del último pago.<br>6. El sistema actualiza la información relacionada con el tiempo sin pagar. |
| **Flujos alternos** | 3a. El pago no se registra: el sistema conserva la fecha del último pago anterior y el tiempo sin pagar continúa aumentando. |
| **Postcondición** | El pago queda registrado en el historial del empeño y la fecha del último pago queda actualizada. |
| **Requisitos que realiza** | RF-004, RF-007, RF-009, RF-011, RNF-CON-002, RNF-CON-003 |


### CU-04 · Calcular el interés de un empeño

| **Campo** | **Contenido** |
|---|---|
| **Actor principal** | Owner / Employee |
| **Objetivo** | Calcular el interés correspondiente a un empeño según los días transcurridos desde el último pago. |
| **Precondición** | El empeño está registrado y cuenta con los datos necesarios para realizar el cálculo. |
| **Escenario principal** | 1. El sistema muestra los campos necesarios para realizar el cálculo junto a los registros del cliente.<br>2. El usuario ingresa manualmente los datos del empeño, como el monto, la tasa de interés y los días transcurridos.<br>3. El sistema verifica que los datos ingresados sean válidos.<br>4. El sistema calcula el interés de forma proporcional a los días transcurridos.<br>5. El sistema muestra al usuario el interés calculado. |
| **Flujos alternos** | 2a. El empeño no tiene pagos anteriores: el sistema utiliza la fecha del empeño para calcular el tiempo transcurrido.<br><br>3a. No hay datos suficientes para realizar el cálculo: el sistema solicita al usuario los datos necesarios antes de mostrar el resultado. |
| **Postcondición** | El sistema muestra el interés calculado para el empeño sin que el usuario tenga que realizar el cálculo manualmente. |
| **Requisitos que realiza** | RF-005, RNF-CON-001 |


### CU-05 · Autorizar un préstamo mayor a $50,000

| **Campo** | **Contenido** |
|---|---|
| **Actor principal** | Owner |
| **Objetivo** | Autorizar un préstamo mayor a $50,000 para permitir que el empeño pueda completarse. |
| **Precondición** | Existe un préstamo mayor a $50,000 pendiente de autorización. |
| **Escenario principal** | 1. El Owner consulta los préstamos pendientes de autorización.<br>2. El sistema muestra la información del préstamo y del empeño.<br>3. El Owner revisa la información.<br>4. El Owner autoriza el préstamo.<br>5. El sistema registra la autorización.<br>6. El sistema permite completar el préstamo. |
| **Flujos alternos** | 4a. El Owner no autoriza el préstamo: el préstamo permanece pendiente y no se completa. |
| **Postcondición** | El préstamo queda autorizado y puede completarse, o permanece pendiente si no fue autorizado. |
| **Requisitos que realiza** | RF-006, RNF-SEG-001 |


### CU-06 · Consultar y gestionar empeños

| **Campo** | **Contenido** |
|---|---|
| **Actor principal** | Owner / Employee |
| **Objetivo** | Consultar los empeños registrados, identificar los que están vencidos y mantener actualizado su estado. |
| **Precondición** | Existen empeños registrados en el sistema. |
| **Escenario principal** | 1. El usuario abre la lista de empeños.<br>2. El sistema muestra los empeños registrados.<br>3. El sistema identifica los empeños que llevan más de tres meses sin pagar intereses.<br>4. El sistema marca en rojo los empeños vencidos.<br>5. El sistema coloca los empeños vencidos al principio de la lista, manteniendo al más antiguo primero.<br>6. El usuario puede revisar la información de cada empeño.<br>7. Cuando corresponde, el usuario actualiza el empeño como inactivo o vendido.<br>8. El sistema guarda el nuevo estado del empeño. |
| **Flujos alternos** | 3a. El empeño todavía no tiene más de tres meses sin pagar: el sistema lo mantiene como activo.<br><br>7a. El cliente continúa con el empeño: el usuario no cambia el estado y el empeño permanece activo. |
| **Postcondición** | Los empeños se muestran organizados de acuerdo con su estado y los empeños que corresponden quedan identificados como activos, vencidos o vendidos. |
| **Requisitos que realiza** | RF-007, RF-011, RNF-CON-003 |


### CU-07 · Consultar el balance de dinero

| **Campo** | **Contenido** |
|---|---|
| **Actor principal** | Owner |
| **Objetivo** | Consultar cuánto dinero se encuentra prestado y cuánto dinero se ha generado mediante los intereses pagados. |
| **Precondición** | Existen préstamos o pagos registrados en el sistema. |
| **Escenario principal** | 1. El Owner abre la sección de balance.<br>2. El sistema consulta los empeños activos y los pagos de intereses registrados.<br>3. El sistema calcula el total de dinero prestado.<br>4. El sistema calcula el total de dinero generado por intereses.<br>5. El sistema muestra ambos balances al Owner. |
| **Flujos alternos** | 2a. No existen préstamos o pagos registrados: el sistema muestra el balance correspondiente en cero. |
| **Postcondición** | El Owner puede consultar el total de dinero prestado y el total de dinero generado por intereses. |
| **Requisitos que realiza** | RF-008, RF-009, RNF-CON-002 |


### CU-08 · Modificar un registro y consultar su historial

| **Campo** | **Contenido** |
|---|---|
| **Actor principal** | Owner / Employee |
| **Objetivo** | Corregir información de un cliente, préstamo o pago sin perder el registro de la modificación realizada. |
| **Precondición** | Existe un registro de cliente, préstamo o pago que necesita ser corregido. |
| **Escenario principal** | 1. El usuario busca el registro que desea corregir.<br>2. El sistema muestra la información actual.<br>3. El usuario modifica el dato incorrecto.<br>4. El sistema guarda el nuevo valor.<br>5. El sistema registra el valor anterior, el valor nuevo, la fecha y el usuario que realizó la modificación.<br>6. El usuario puede consultar el historial de modificaciones del registro. |
| **Flujos alternos** | 3a. El usuario no realiza ningún cambio: el sistema conserva la información original.<br><br>5a. Se intenta modificar una entrada del historial: el sistema no permite modificar ni eliminar la entrada registrada. |
| **Postcondición** | El registro queda corregido y el historial conserva la información anterior y la nueva, junto con la fecha y el usuario que realizó el cambio. |
| **Requisitos que realiza** | RF-010, RNF-SEG-002, RNF-CON-003 |

---

## 6. Trazabilidad

| Requisito       | Origen                                                                                 | Caso de uso                | Elemento del prototipo |
| --------------- | -------------------------------------------------------------------------------------- | -------------------------- | ---------------------- |
| RF-001          | Visión (alcance); entrevista del 22 de septiembre, Proceso actual                      | Por definir (semana 7)     | Por definir            |
| RF-002          | Visión (alcance); entrevista del 22 de septiembre, Proceso actual                      | Por definir (semana 7)     | Por definir            |
| RF-003          | Visión (regla de negocio 3); ficha de dominio del guion del 22 de septiembre           | Por definir (semana 7)     | Por definir            |
| RF-004          | Visión (fuera del alcance); entrevista del 22 de septiembre, Proceso actual            | Por definir (semana 7)     | Por definir            |
| RF-005          | Visión (alcance, regla de negocio 1); entrevista del 22 de septiembre, Proceso actual  | Por definir (semana 7)     | Por definir            |
| RF-006          | Visión (conflicto entre usuarios); entrevista del 22 de septiembre, Excepciones        | Por definir (semana 7)     | Por definir            |
| RF-007          | Visión (alcance, regla de negocio 2); entrevista del 22 de septiembre, Dolores         | Por definir (semana 7)     | Por definir            |
| RF-008          | Visión (alcance)                                                                       | Por definir (semana 7)     | Por definir            |
| RF-009          | Visión (descripción); entrevista del 22 de septiembre, Dolores                         | Por definir (semana 7)     | Por definir            |
| RF-010          | Visión (alcance)                                                                       | Por definir (semana 7)     | Por definir            |
| RF-011          | Visión (alcance)                                                                       | Por definir (semana 7)     | Por definir            |
| RNF-CON-001     | Visión (atributos de calidad); entrevista del 22 de septiembre, Dolores                | Por definir (semana 7)     | Por definir            |
| RNF-CON-002     | Visión (atributos de calidad)                                                          | Por definir (semana 7)     | Por definir            |
| **RNF-CON-003** | **Guion de entrevista del 22 de septiembre, ficha de dominio**                         | **Por definir (semana 7)** | **Por definir**        |
| RNF-SEG-001     | Visión (atributos de calidad, conflicto); entrevista del 22 de septiembre, Excepciones | Por definir (semana 7)     | Por definir            |
| RNF-SEG-002     | Visión (atributos de calidad, usuarios)                                                | Por definir (semana 7)     | Por definir            |
| **RNF-USA-001** | **Visión (usuarios)**                                                                  | **Por definir (semana 7)** | **Por definir**        |

---

## 7. Registro de cambios

| Fecha      | Requisito | Qué cambió                    | Por qué         |
| ---------- | --------- | ----------------------------- | --------------- |
| 29/09/2026 | Todos     | Primera versión del documento | Entrega inicial |

---

## Antes de entregar

- [ ] Todos los requisitos tienen identificador único y ninguno está repetido
- [ ] Cada requisito expresa una sola idea
- [ ] Cada requisito funcional tiene criterio de aceptación comprobable
- [ ] Cada requisito no funcional tiene una métrica, no solo un adjetivo
- [ ] El campo Origen distingue lo confirmado por el cliente de lo que sigo suponiendo
- [ ] Hay al menos un requisito no funcional por cada atributo de calidad que impone mi tipo de sistema
- [ ] Ningún requisito impone una solución técnica
- [ ] Todos los requisitos caben dentro del alcance declarado
- [ ] La tabla de trazabilidad está completa
- [ ] Mi dupla revisó el documento y su revisión está registrada
- [ ] Borré los ejemplos y las instrucciones en cursiva
