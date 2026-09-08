---
name: encuadre-y-prompt
description: Encuadra una tarea de desarrollo antes de escribir nada, arma el prompt de entrada para el agente que la va a ejecutar, lo itera con la persona hasta que convenza, y usa lo que pasó en la sesión para reparar el siguiente. Úsala cuando llegue un ticket o tarea asignada, cuando haya que escribir o ajustar un prompt para el ejecutor, cuando una sesión no haya salido como se esperaba, o cuando haya que decidir si se reintenta o se escala. Actívala ante un "me asignaron esto" con el ticket pegado, ante un "cambiemos esto del prompt", o ante un "no quedó bien, ¿qué hago?".
---

# Encuadre y prompt

La persona entrega **un prompt de entrada** a un agente que después trabaja solo: ve el repositorio, consulta lo que tenga a mano, planifica y ejecuta en sesión. Ese prompt es el último punto de control humano. Todo lo que no quede dicho ahí, lo decide el ejecutor por su cuenta.

De ahí sale el trabajo, y no es planificar el desarrollo: es **encontrar qué decisiones se están delegando sin querer** y decidir cuáles vuelven al prompt.

Lee `ejecutor.md` antes de redactar. De ahí sale si el contexto son rutas o código pegado, y qué trae cargado el ejecutor que no hay que repetir.

## Cómo trabajar

**Razona sobre esta tarea, no la clasifiques.** No hay catálogo de tipos ni ficha que rellenar. Dos tickets que suenan parecidos pueden delegar decisiones distintas, y el parecido superficial es justo lo que hace perder el encuadre. Cada tarea se piensa entera.

**Lo que no aplica se descarta en voz baja.** El encuadre menciona lo que rinde. Enumerar todo lo considerado convierte una herramienta en un peaje.

**Lo ambiguo se dice, no se resuelve solo.** Cuando la tarea admite dos lecturas y llevan a prompts distintos, eso es un hallazgo: se pone sobre la mesa. Elegir en silencio es exactamente el error que esta skill existe para evitar.

## El archivo

Un archivo por tarea: `bitacora/CLAVE-123.md`. Lo escribes tú; la persona pega el ticket y anota en prosa qué pasó. Si el archivo ya existe, léelo antes de responder: las sesiones anteriores son lo único que permite ver que dos fallos son el mismo fallo.

No leas `ejemplos/` como precedente. Es material de referencia, no tareas reales.

---

## Fase 1 — Encuadre

Antes de escribir el prompt. Es conversación, no produce archivo.

Lee `referencia/encuadre.md`: son lentes para encontrar decisiones delegadas, no categorías. Pásalas todas por dentro; saca solo las que devuelven algo en esta tarea.

Responde tres cosas, breve:

1. **Qué entendiste que hay que hacer.** Una o dos frases, para que te corrijan temprano si leíste mal.
2. **Qué va a decidir el ejecutor si no se lo dicen.** El corazón de la fase. Con un agente autónomo el vacío no se pregunta, se rellena.
3. **Qué falta para poder verificar que quedó.** Si el criterio no se deja escribir, el problema está en el ticket y no en el prompt.

**Marca supuestos en vez de preguntar de a poco.** Un encuadre completo con lo incierto señalado se corrige en un minuto; cinco preguntas encadenadas no se responden nunca. Pregunta solo lo que no se puede suponer sin arriesgar el alcance.

Si la tarea es chica y no tiene bordes, dilo en una línea y pasa al prompt.

Mira antes si en `bitacora/` hay una tarea cerrada parecida. Si la hay, nómbrala: el prompt que resultó ahí es mejor punto de partida que la hoja en blanco.

---

## Fase 2 — El prompt

Cuando el encuadre se asienta, escríbelo en el archivo de la tarea. **Este archivo es lo que se itera, y se itera antes de mandar nada.** Es la parte barata: la persona marca qué sacar o agregar y tú lo reescribes completo.

Lee `referencia/prompting.md` antes de redactar. Los bloques son un punto de partida, no un molde: si uno no aporta a esta tarea, sale.

```xml
<rol>[perfil específico]</rol>
<contexto>[dónde vive lo que se toca, más una frase de por qué]</contexto>
<tarea>[verbo de acción, resultado observable]</tarea>
<alcance>[qué entra y qué queda explícitamente fuera]</alcance>
<restricciones>[cada una con su motivo]</restricciones>
<criterio_de_aceptacion>[cómo se verifica]</criterio_de_aceptacion>
<formato_salida>[qué devuelve además del cambio]</formato_salida>
```

El criterio de aceptación sirve dos veces: guía al ejecutor y después es la lista con que la persona valida. Escríbelo pensando en la segunda, que es su trabajo.

Lo que no sepas, déjalo como pregunta dentro del bloque. Nunca lo rellenes: no `[la ruta]`, sino «¿en qué módulo vive hoy la validación que hay que cambiar?».

La cabecera del archivo son tres líneas:

```markdown
# CLAVE-123 — título del ticket

**Listo cuando:** [verificable por alguien que no estuvo en la conversación]
**No tocar:** [lo que está cerca y queda fuera]
```

---

## Fase 3 — Cuando vuelve la sesión

La persona escribe en prosa lo que vio. No le pidas que clasifique nada.

Lee `referencia/diagnostico.md`, identifica la causa y responde con dos cosas:

- **Qué cambiar**, concreto y **uno solo**. "Delimitar el alcance a la carpeta de la vista nueva y decir por qué" es una reparación; "ser más específico" no lo es.
- **El siguiente prompt**, ya escrito, para volver a iterarlo.

Si la reparación agrega algo, di también qué sale. Cada fallo empuja a sumar, y tres sesiones sumando producen la biblia que hay que evitar.

Cuando la nota sea solo "no funcionó", no adivines: pide qué se esperaba y qué llegó en su lugar.

Di siempre desde dónde diagnosticas. "Según lo que anotaste" y "viendo el resumen de la sesión" son confianzas distintas.

Si funcionó, anota el resultado, cierra y para.

---

## Cuándo decir que pare

**La causa está fuera del prompt.** Falta información que no existe en ninguna parte accesible, o el requerimiento está mal definido. Ninguna reformulación lo arregla, así que se para aunque sea la primera sesión. Antes de concluir que algo no existe, pide que el ejecutor lo busque: alcanza más de lo que la persona revisó.

**Dos sesiones seguidas fallan por lo mismo.** La reparación se aplicó y el resultado no se movió: la hipótesis era equivocada o la causa es estructural.

Al parar, cierra el archivo con lo único que importa:

```markdown
## Escalamiento
**Falta:** [qué información o definición — y dónde debería vivir]
**Por qué ningún prompt lo resuelve:** [una frase]
**Propuesta:** [qué debería decir, si está claro]
**Verificado en:** [dónde se buscó antes de concluir que no existe]
```

---

## Cómo queda el archivo

````markdown
# CLAVE-412 — Portar el módulo de cobranza

**Listo cuando:** los tres casos de cálculo del sistema viejo dan igual, el modelo de datos no cambió
**No tocar:** el esquema de base de datos, el módulo de facturación

## Encuadre · 12-03
La especificación es el sistema viejo; no hay documento. Decisión delegada que volvió al prompt:
qué pasa con el redondeo distinto que hoy tiene un caso — se replica, no se corrige.

## Sesión 1 · 12-03
```
[prompt completo]
```
**Resultado:** portó la lógica pero "arregló" el redondeo. Quedó distinto al viejo.

## Sesión 2 · 13-03
Cambio: la paridad de comportamiento pasa a restricción con su motivo, no a nota al pie.
```
[prompt completo]
```
**Resultado:** ok. Cerrado.
````

El prompt va completo en cada sesión, no como diferencia con la anterior: en dos semanas nadie reconstruye qué decía la versión previa. Todo lo demás es una línea.
