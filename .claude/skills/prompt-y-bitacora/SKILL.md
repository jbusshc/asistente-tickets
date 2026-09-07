---
name: prompt-y-bitacora
description: Convierte una tarea de Jira en un prompt acotado, y a partir de lo que la persona anota que pasó, propone el siguiente prompt o le dice que pare. Mantiene un solo archivo por tarea con los prompts usados y los resultados observados. Úsala cuando llegue un ticket o tarea asignada, cuando haya que escribir o recortar un prompt, cuando algo no haya salido como se esperaba y toque decidir si reintentar, o cuando haya que armar el caso para escalar. Actívala ante un "me asignaron esto" con el ticket pegado, o ante un "falló, ¿qué hago?".
---

# Prompt y bitácora

El trabajo de la persona es **decidir el contexto mínimo suficiente** y observar el resultado. Esta skill escribe el prompt y lleva el registro; el juicio sobre qué contexto entregar es suyo, porque exige mirar el código.

Todo el registro es **un solo archivo por tarea**: `bitacora/CLAVE-123.md`. No hay carpetas, ni estado en JSON, ni plantillas que llenar. Si usar esto cuesta más que no usarlo, no sirve.

## Qué sabe y qué no

No conoce el sistema que ejecuta la tarea, no interactúa con él y no ve el repositorio. Trabaja con el ticket y con lo que la persona anota.

Nunca rellenes un campo que exija haber mirado algo. Déjalo como pregunta concreta: no `[material]`, sino «¿qué procedimiento tiene la lógica que hay que cambiar y qué tipos usa?».

## Cuando llega el ticket

Genera dos cosas y nada más:

**1. El prompt.** Acotado a la tarea. Este es el entregable real.

Lee `referencia/prompting.md` antes de redactarlo. Los bloques son:

```xml
<rol>[perfil específico]</rol>
<estandares>[solo las reglas que aplican a este cambio]</estandares>
<material>[lo que se toca + lo que define su contrato]</material>
<tarea>[verbo de acción, resultado observable, una unidad]</tarea>
<restricciones>[cada una con su motivo]</restricciones>
<formato_salida>[qué debe volver]</formato_salida>
```

El material va antes de la tarea: la atención se degrada en el medio del contexto y conviene que la instrucción sea lo último que se lee.

Tres líneas que casi siempre valen su espacio, y que la referencia explica: el verbo de la tarea tiene que pedir acción y no sugerencia; hay que decirle que no especule sobre código que no recibió; y en cambios de código, que no haga de más.

Lo que no sepas, déjalo como pregunta dentro del bloque. La persona lo completa mirando el sistema.

**2. La cabecera de la bitácora.** Tres líneas, no una especificación:

```markdown
# CLAVE-123 — título del ticket

**Listo cuando:** [criterio verificable por alguien que no estuvo en la conversación]
**No tocar:** [lo que está cerca y queda fuera]
```

Si el ticket no trae criterio de aceptación, dilo en una línea. Un ticket sin criterio no es un problema de prompt: si además la descripción admite lecturas distintas, aclararlo con quien lo escribió sale más barato que gastar intentos.

## El contexto mínimo

Es lo que define el oficio, así que aplícalo al redactar en vez de convertirlo en un checklist.

La regla: **cada pieza de material tiene que responder a algo del criterio o de las restricciones.** Si no se puede nombrar a qué, sobra.

Tres clases, con destinos distintos:

- **Lo que se modifica** — va completo.
- **Lo que define su contrato** (firmas, tipos, DDL de lo que toca) — va solo la parte que se usa.
- **Lo que explica el porqué** — no se adjunta. Se resume en una frase dentro de la tarea. Adjuntar documentación de contexto es la forma más común de inflar un prompt sin mejorarlo.

Ante la duda sobre una pieza, déjala fuera. Agregarla en el intento 2 es barato; descubrir que ahogó la instrucción no.

## Cuando la persona anota qué pasó

Escribe en prosa lo que vio. No le pidas que clasifique nada ni que llene un formulario: la clasificación es tuya y va por dentro.

Lee `referencia/diagnostico.md`, identifica la causa y responde con dos cosas:

- **Qué cambiar**, concreto y **uno solo**. "Agregar el patrón de manejo de errores y la restricción de usarlo" es una reparación; "ser más específico" no lo es.
- **El siguiente prompt**, ya escrito.

Si la reparación agrega algo, di también qué sale. Cada fallo empuja a sumar, y tres intentos de sumar producen la biblia que hay que evitar. Si el prompt creció y el resultado empeoró, sospecha de exceso de material antes que de nada.

Cuando la nota sea solo "no funcionó", no adivines una causa. Pide lo mínimo para diagnosticar: qué se esperaba y qué llegó en su lugar.

Di siempre desde dónde estás diagnosticando. "Según lo que anotaste" y "viendo la salida" son niveles de confianza distintos.

## Cuándo decir que pare

Dos señales, y conviene decirlas sin rodeos:

**La causa está fuera del prompt** — falta información que no existe documentada en ninguna parte, no hay estándar que seguir, o el requerimiento está mal definido. Ninguna reformulación lo arregla. Se para aunque sea el primer intento: eso no es rendirse temprano, es haber identificado que el problema no está en cómo se pide.

**Dos intentos seguidos fallan por lo mismo** — la reparación se aplicó y el resultado no se movió. La hipótesis era equivocada o la causa es estructural.

Al parar, agrega al final del archivo un cierre corto. Lo único que importa es la propuesta:

```markdown
## Escalamiento
**Falta:** [qué información, estándar o definición — y dónde debería vivir]
**Por qué ningún prompt lo resuelve:** [una frase]
**Propuesta:** [qué debería decir, si está claro]
**Verificado en:** [dónde se buscó antes de concluir que no existe]
```

Antes de mandar a escalar, pregunta dónde buscó. Escalar algo que sí existía desgasta a quien recibe esos casos.

## Cómo queda el archivo

```markdown
# CLAVE-123 — Aplicar descuento a clientes preferentes

**Listo cuando:** compila, la prueba con cliente sin categoría pasa, el porcentaje no queda fijo en el código
**No tocar:** el cálculo de impuestos

## Intento 1 · 12-03
```
[prompt completo]
```
**Resultado:** aplicó el descuento pero revienta si el cliente no tiene categoría. No manejó el null.

## Intento 2 · 12-03
Cambio: agregado el estándar de manejo de excepciones + restricción de usarlo.
```
[prompt completo]
```
**Resultado:** ok. Cerrado.
```

El prompt va completo en cada intento, no como diferencia con el anterior: en dos semanas nadie reconstruye qué decía la versión previa. Todo lo demás es una línea.
