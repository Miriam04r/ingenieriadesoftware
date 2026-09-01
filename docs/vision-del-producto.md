# Visión del producto



**Autor:** Miriam Gómez Mariscal

**Fecha de la última versión:** 18/08/2026

**Repositorio:** Ingeniería de Software 

---

## 1. Descripción del sistema



**Nombre del sistema:** EmpeñoControl

**Descripción:** EmpeñoControl será un sistema que ayudará a administrar una casa de empeño, permitiendo registrar clientes, préstamos y objetos dejados como garantía. También llevará el control de pagos, calculará automáticamente los intereses y mostrará que clientes tienen pagos pendientes, cuánto tiempo llevan sin pagar y que empeños ya están vencidos.

---

## 2. Problema y usuarios



**El problema:** Al llevarse el control de la casa de empeño de forma manual, han llegado a ocurrir problemas en los cálculos de intereses y en ocasiones no se detecta a tiempo cuando un cliente lleva más de tres meses sin realizar un pago, lo que resulta en pérdidas de dinero. Además, al no contar con un registro digital de los empeños vencidos, si llegara a faltar alguno, sería difícil detectarlo y llevar un control adecuado sobre ellos.

**Cómo se resuelve hoy sin el sistema:** Toda la información se registra en libretas, hojas y anotaciones hechas a mano. Los intereses también se calculan manualmente, y el seguimiento de los pagos depende de revisar los registros para saber que clientes han pagado y cuáles tienen adeudos.

**Usuarios del sistema:**

| Tipo de usuario | Qué necesita del sistema | Qué le preocupa |
|---|---|---|
|Owner |Supervisar clientes, préstamos, pagos y ganacias  |Perder información o que un error sea irreversible|
|Employee |Registrar datos y calcular intereses automáticamente |Que sea difícil de usar o registrar datos incorrectos |



**Un conflicto entre usuarios:** El employee puede querer realizar un préstamo de cualquier cantidad para agilizar la atención al cliente, mientras que el Owner quiere tener mayor control sobre los préstamos de cantidades altas. Por ello, cuando un préstamo supere los $50,000 pesos, el sistema requerirá la autorización del Owner antes de completar la operación



---

## 3. Alcance

### Dentro del alcance

- Calcula impuestos ingresando los datos del cliente
- Hace un balance de cuanto dinero tiene prestado el owner y cuánto dinero le está generando
- Permite hacer un registro manual de cada cliente con su información 
- Subraya a los clientes que están atrasados en pagos de color rojo y los manda arriba de la lista manteniendo al más atrasado al principio
- Mantiene un historial de las modificaciones realizadas en los registros

### Explícitamente fuera del alcance

- No calcula el impuesto de cada cliente por si solo, si no que cuando se necesita saber se ingresan los datos y se calcula
- No manda un aviso de cuando un cliente se atrasó con el pago
- El estado de los pagos no se actualiza automáticamente

**Por qué queda fuera:** No calcula los intereses automáticamente porque el monto depende del valor del préstamo y de los días transcurridos desde el último pago, por eso los datos deben ingresarse cuando se necesite realizar el cálculo.


---

## 4. Tipo de sistema y restricciones

**Tipo de sistema:** De información 

**Por qué es de ese tipo:** Porque permite registrar, almacenar, consultar y gestionar información de la casa de empeño, como datos de clientes, préstamos, garantías y pagos. También procesa esta información para calcular intereses, llevar el control de adeudos y mostrar el estado de los empeños.

**Atributos de calidad que impone:**

| Atributo | Por qué importa en mi caso | Qué pasa si no se cumple |
|---|---|---|
|Exactitud | El sistema debe realizar correctamente los cálculos de intereses, pagos y refrendos|Se podrían cobrar cantidades incorrectas y generar pérdidas de dinero o problemas con los clientes |
|Seguridad |La información de clientes, préstamos y dinero debe estar protegida y cada usuario debe tener permisos de acuerdo con su función. |Un empleado podría modificar información que no debería o se podría perder información importante|
|Integridad de los datos |La información de los clientes, préstamos y pagos debe mantenerse correcta y consistente |Podrían existir registros duplicados, información incorrecta o diferencias entre el dinero registrado y el dinero real |

**Reglas de negocio que ya identifiqué:**

1. Los intereses se calculan proporcionalmente según los días transcurridos
2. El empeño se considera vencido después de tres meses sin pagar interés 
3. El cliente puede tener más de un empeño activo a la vez

---

## 5. Ciclo de vida elegido

**Modelo elegido:** Ágil

**Por qué le conviene a este proyecto:** Ágil es adecuado para EmpeñoControl porque algunos requisitos pueden cambiar al probar el sistema con el Owner y el Employee. Al ser un proyecto pequeño y con un riesgo principalmente económico, se pueden desarrollar y entregar las funciones por partes, recibir retroalimentación y realizar cambios conforme avance el proyecto

### Alternativas descartadas

**Alternativa 1:** Prototipado

**Por qué la descarté:** Porque se enfoca principalmente en validar el diseño y la interacción con el usuario, mientras que EmpeñoControl necesita desarrollar varias funciones completas y mejorarlas progresivamente

**Alternativa 2:** Cascada

**Por qué la descarté:** Porque requiere que los requisitos estén definidos y sean estables desde el inicio y en EmpeñoControl pueden surgir cambios conforme el Owner y el Employee prueben el sistema, por lo que es más conveniente utilizar un modelo flexible

---

## Antes de entregar

Reviso que el documento cumpla lo siguiente:

- [ ] La descripción del apartado 1 se entiende sin ser del área
- [ ] Hay al menos dos tipos de usuario con necesidades distintas
- [ ] Identifiqué un conflicto real entre usuarios
- [ ] El alcance dice qué queda fuera, no solo qué queda dentro
- [ ] Las exclusiones son específicas, no genéricas
- [ ] Identifiqué el tipo de sistema y al menos dos atributos de calidad
- [ ] Anoté al menos tres reglas de negocio no obvias
- [ ] Justifiqué el ciclo de vida contra dos alternativas descartadas
- [ ] El documento está en mi repositorio y se puede leer desde el navegador
- [ ] Borré todas las instrucciones en cursiva de la plantilla
