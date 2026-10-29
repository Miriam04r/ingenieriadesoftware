# ADR-001: Monolito modular en lugar de microservicios

## Estado
Aceptada, 29 de octubre de 2026

## Contexto
El sistema EmpeñoControl[cite: 3] está siendo construido por una sola persona[cite: 2]. El sistema agrupa sus reglas de negocio en tres módulos principales: clientes, empeños y finanzas[cite: 1]. Actualmente, las fronteras entre estos módulos están bien definidas y separadas, pero siguen necesitando comunicarse entre sí de forma constante[cite: 2]. Por ejemplo, el módulo de finanzas necesita comunicarse con empeños para revisar los préstamos y calcular los balances[cite: 1].

## Decisión
Construimos un monolito modular[cite: 1]: un solo desplegable que mantiene la separación lógica de los tres módulos por carpetas e interfaces, asegurando que la comunicación entre ellos se mantenga ordenada.

## Consecuencias
Siguiendo la ley de Conway, al ser un sistema construido por una sola persona y no por múltiples equipos desarrolladores, evitamos la sobrecarga técnica y operativa que implicaría dividir el sistema en microservicios[cite: 2]. 

Si en el futuro el módulo de finanzas empieza a requerir actualizaciones mucho más frecuentes, como modificaciones constantes en las fórmulas de interés o la solicitud de nuevos reportes financieros, será el primer módulo en extraerse hacia un servicio independiente[cite: 2].

El riesgo principal es que, por rapidez, se rompan las reglas y un módulo acceda directamente a la base de datos de otro. Los límites entre módulos se revisarán estrictamente a nivel de código durante el desarrollo.
