# SC-001: Recordatorio de vencimiento por WhatsApp

---

## Estado
Propuesta · 16/11/2026

## Quién la pide
Dupla de revisión (simulando al Owner del negocio).

## Qué se pide
Quiero que el sistema le mande un mensajito automático por WhatsApp al cliente unos tres días antes de que su empeño cumpla los tres meses, para avisarle que está a punto de vencer y evitar que pierda sus cosas por un simple olvido.

## Por qué
Muchos clientes se enojan cuando regresan y sus cosas ya se vendieron porque se les pasó la fecha por un par de días. Si les avisamos antes, mejoramos el servicio al cliente, generamos confianza y aseguramos que vengan a pagar sus intereses, lo que nos da liquidez.

## Qué pasa si no se hace
Seguiremos teniendo roces con clientes olvidadizos y perderemos la oportunidad de cobrar esos intereses antes de tener que pasar por el proceso largo de poner el objeto a la venta.

## Tipo de mantenimiento
- [ ] **Correctivo** · algo está mal y hay que repararlo
- [ ] **Adaptativo** · el entorno cambió y hay que ajustarse
- [x] **Perfectivo** · funciona, pero puede ser mejor
- [ ] **Preventivo** · todavía no falla, pero va a fallar

**Justificación:** El sistema funciona correctamente para calcular el vencimiento, pero agregar este aviso mejora la experiencia del negocio.

## Criterio de aceptación
Cuando falten exactamente 3 días para que un empeño cumpla 3 meses sin pagos, el cliente debe recibir un mensaje de WhatsApp automático con el recordatorio.

## Prioridad que sugiere el solicitante
Media. No detiene la operación actual de la casa de empeño, pero ayudaría mucho a retener clientes.
