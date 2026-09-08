# asistente-prompts-dev

Encuadra una tarea de desarrollo, arma el prompt de entrada para el agente que la va a ejecutar, lo itera contigo y usa lo que pasó en la sesión para reparar el siguiente.

No escribe código ni lo ejecuta. Eso lo hace el ejecutor.

## Para qué

El ejecutor trabaja solo: ve el repositorio, consulta lo que tenga a mano, planifica y desarrolla en sesión. **El prompt de entrada es el último punto de control humano.** Después de mandarlo no se maneja el proceso, y todo lo que no quedó dicho lo decide él.

El trabajo, entonces, no es planificar el desarrollo. Es encontrar qué decisiones se están delegando sin querer y decidir cuáles vuelven al prompt.

## No clasifica tareas

No hay catálogo de tipos ni ficha que rellenar. Encasillar una tarea hace heredar los puntos ciegos de las casillas que no se abrieron, y dos tickets que suenan parecidos delegan decisiones distintas.

En su lugar hay lentes: formas de mirar cualquier tarea para encontrar qué va a decidir el ejecutor si nadie se lo dice. Se pasan todas y salen solo las que devuelven algo. Una lente vacía es gratis; una categoría no elegida es un punto ciego.

## El ciclo

1. **Pegas el ticket.** La skill se activa sola.
2. **Encuadre.** Antes de escribir nada, te dice qué entendió, qué va a decidir el ejecutor si no se lo dices y qué falta para poder verificar. Con supuestos marcados para que los corrijas, no como interrogatorio. Si la tarea es chica, lo dice en una línea y sigue.
3. **El prompt.** Se escribe en `bitacora/CLAVE-123.md`. Ese archivo es lo que iteras: marcas qué sacar o agregar y lo reescribe completo. Es la parte barata, así que aquí se gasta el tiempo.
4. **Lo mandas al ejecutor.**
5. **Vuelves y anotas en prosa qué pasó.** Te devuelve una reparación concreta y el siguiente prompt, o te dice que pares y arma el caso para escalar.

Una sesión completa cuenta como un intento, no cada mensaje dentro de ella.

## Ejemplos

En `ejemplos/`, tres casos completos con la conversación tal como ocurre:

- `01-portar-modulo.md` — el encuadre saca a la luz una decisión que el ticket delegaba en silencio.
- `02-tarea-chica.md` — sin bordes: encuadre en una línea, prompt de cuatro bloques.
- `03-cuando-no-se-escribe-prompt.md` — se para antes de la primera sesión y se escala.

La skill no lee esta carpeta como precedente.

## Cuándo te va a decir que pares

- **La causa está fuera del prompt** — falta algo que no existe en ninguna parte accesible, o el requerimiento está mal definido. Ninguna reformulación lo arregla, así que se para aunque sea la primera sesión.
- **Dos sesiones seguidas fallan por lo mismo** — la reparación se aplicó y el resultado no se movió.

Antes de dar algo por inexistente, te pide que el ejecutor lo busque: alcanza más de lo que tú revisaste.

## Estructura

```
ejecutor.md                     qué agente recibe el prompt y qué trae puesto
.claude/skills/encuadre-y-prompt/
  SKILL.md                      el flujo
  referencia/encuadre.md        lentes para encontrar decisiones delegadas
  referencia/prompting.md       cómo se redacta
  referencia/diagnostico.md     cómo se lee lo que pasó en la sesión
bitacora/CLAVE-123.md           un archivo por tarea
ejemplos/                       casos de uso
```

## `ejecutor.md` es lo primero que se edita

Ahí está descrito el agente: si ve el repositorio, qué trae cargado, si escribe en el código. De eso depende la forma del prompt — con acceso al repositorio el contexto son rutas, sin acceso es código pegado. Son dos prompts distintos.

Es el único archivo que cambia si cambias de agente. El método no se toca.

## La bitácora

Un archivo por tarea. Sin carpetas, sin estado en JSON, sin plantillas. El prompt va completo en cada sesión y no como diferencia con la anterior, porque en dos semanas nadie reconstruye qué decía la versión previa. Todo lo demás es una línea.

El criterio que ordena el diseño: si usarlo cuesta más que no usarlo, no sirve.
