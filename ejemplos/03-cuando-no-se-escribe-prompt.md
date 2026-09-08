# Ejemplo 3 — Cuando no se escribe prompt

El caso menos obvio: el asistente para antes de la primera sesión. No es rendirse temprano, es haber identificado que el problema no está en cómo se pide.

Ticket inventado.

---

## La persona pega el ticket

> CLAVE-508 — El descuento se aplica mal a clientes antiguos
> Usuarios reportan que a algunos se les cobra de más. Revisar el cálculo.

## El asistente encuadra

**Qué entiendo:** un cálculo de descuento da un resultado incorrecto para un subconjunto de clientes que no está identificado.

**Qué va a decidir el ejecutor si no se lo decimos:**

- **Cuál es el comportamiento correcto.** El ticket dice que está mal, no qué debería dar. Va a deducir la regla del código — y si el código es el bug, deduce el bug.
- Si arregla el síntoma o va a la raíz.
- Qué pasa con los cobros ya emitidos con el valor incorrecto.

**Qué falta para verificar:** todo. No hay caso de reproducción ni valor esperado.

> **Antes de escribir nada:** ¿tienes un cliente concreto donde falle, y cuánto debería cobrarse en ese caso?

## La persona responde

> No, solo el reporte. Y la regla para clientes antiguos nadie la tiene clara, viene de un acuerdo comercial viejo.

## El asistente para

No se escribe prompt. Lo que falta no está en el repositorio ni en la base de conocimiento: está en un acuerdo que nadie transcribió. Un prompt que pida deducir la regla produce un cálculo que se ve razonable y que nadie puede validar — peor que el bug, porque pasa desapercibido.

Antes de escalar, la pregunta obligatoria:

> Pídele al ejecutor que busque la regla en el repositorio y en la base de conocimiento. Alcanza más de lo que revisaste.

Se busca y no aparece.

## Cierre del archivo

```markdown
## Escalamiento
**Falta:** la regla de descuento para clientes antiguos. Debería vivir en la
base de conocimiento del módulo de facturación.
**Por qué ningún prompt lo resuelve:** sin valor esperado, cualquier
implementación es defendible y ninguna verificable.
**Propuesta:** obtener la regla de quien administra el acuerdo comercial y
dejarla escrita antes de reabrir el ticket.
**Verificado en:** repositorio y base de conocimiento, vía el ejecutor.
```

---

Es el caso que más tiempo ahorra y el que menos se siente como avance. Un ticket así puede consumir tres o cuatro sesiones produciendo cálculos plausibles antes de que alguien note que nadie sabe cuál es el correcto.
