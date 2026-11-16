# Análisis de impacto de SC-001

---

## Solicitud que se analiza
Referencia a la solicitud: `sc-001-recordatorio-whatsapp.md`, solicitada por la Dupla de Revisión el 16/11/2026.

## Traducción a términos del sistema
El sistema necesita un proceso programado (cron job) en la API Node.js que consulte diariamente la base de datos buscando registros de la clase `Empeno` donde la diferencia entre la fecha actual y la `fechaUltimoPago` (o `fechaEmpeno`) sea exactamente de 87 días. Se debe crear un nuevo módulo/componente `Notificador` que se integre con una API externa (Meta/WhatsApp) para enviar el mensaje utilizando el atributo `telefono` de la clase `Cliente`.

## Impacto directo
Lo que la solicitud toca por definición: lo que hay que modificar para que el cambio exista.

| Artefacto | Unidad | Qué hay que cambiar |
|---|---|---|
| Requisito RF-012 (Nuevo) | 2 | Agregar requisito funcional para el envío de notificaciones. |
| Requisito Fuera de Alcance | 2 | Eliminar la exclusión que decía explícitamente "No manda un aviso de cuando un cliente se atrasó con el pago". |
| Caso de uso (Nuevo) | 2 | Crear CU-09: "Notificar próximo vencimiento". |
| Diagrama de clases | 4 | Agregar la clase `Notificador` o el servicio externo, y un método `revisarProximosVencimientos()` en el gestor de empeños. |
| Diagrama de secuencia | 4 | Crear un diagrama nuevo para el escenario del proceso automático nocturno enviando el mensaje. |

## Impacto indirecto
Lo que se rompe o deja de ser cierto por culpa del cambio directo.

| Artefacto | Unidad | Por qué se ve afectado |
|---|---|---|
| Registro de decisión ADR-001 | 3 | Sin impacto (la arquitectura Monolito Modular soporta agregar un módulo de notificaciones sin volverse microservicios). |
| Diagrama de contenedores C4 | 3 | Hay que agregar un nuevo sistema externo ("WhatsApp API") y una flecha saliendo desde la API Node.js hacia él. |
| Máquina de estados | 4 | Sin impacto (el estado del empeño sigue siendo "Activo" cuando se envía el recordatorio, no cambia de estado). |
| RNF-CON-003 (Integridad) | 2 | Afectado. Se requiere validar que el atributo `telefono` del `Cliente` se guarde a 10 dígitos obligatoriamente para que la API de WhatsApp no falle. |

## Lo que queda sin tocar
El cálculo de intereses (RF-005), las reglas de negocio de vencimiento a los 3 meses (RF-007), los balances de finanzas (RF-008, RF-009) y el registro manual de pagos (RF-004) se mantienen exactamente igual. No se altera la base de datos actual, solo se consulta.

## Riesgos
1. **Riesgo técnico:** Depender de la API de WhatsApp Business requiere configuraciones de Meta, plantillas aprobadas y costos por mensaje. 
2. **Riesgo de datos:** Actualmente el teléfono se captura como `string` libre. Si el Employee anota "no tiene" o un teléfono falso, el sistema externo arrojará errores diarios.

## Alternativas consideradas
1. **Opción A (La solicitada):** Integrar WhatsApp Business API con un cron job automático. **Implica:** Costos recurrentes, alta complejidad de configuración y modificar el alcance del proyecto.
2. **Opción B (Alternativa local):** En lugar de mensajes automáticos, agregar una "Alerta Visual" en el Dashboard del Owner/Employee mostrando una lista de "Empeños a vencer en 3 días". **Implica:** Cero dependencias externas, respeta el alcance original (todo es gestión manual) y el empleado puede mandar el mensaje desde el celular del negocio.

## Estimación de esfuerzo

| Concepto | Esfuerzo |
|---|---|
| Cambios de diseño y documentación | 4 horas |
| Implementación (Opción A completa) | 35 horas |
| Pruebas (Unitarias y de API) | 10 horas |
| **Total** | **49 horas** |

**De dónde sale este número:** 
Comparado con el módulo de registro de empeños que tomó aprox. 15 horas, integrar una API externa de terceros (Meta), tramitar los tokens, manejar las caídas de red (reintentos) y probar un cron job asíncrono es más del doble de complejo. La estimación supone que la empresa está dispuesta a pagar la cuenta de desarrollador de WhatsApp.

## Recomendación
**Rechazar la Opción A y proponer la Opción B.** 
Justificacion: El alcance original y la visión del producto definen que este es un sistema de gestión manual para una casa de empeño pequeña. El costo de desarrollo y mantenimiento de una API oficial de mensajería supera el presupuesto de este tipo de negocio. La Opción B resuelve la necesidad de negocio (evitar que los clientes olviden su fecha) respetando la arquitectura, sin depender de sistemas externos y costaría menos de 8 horas implementar.
