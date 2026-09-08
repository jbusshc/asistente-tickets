# Encuadre

Para el asistente. Sirve para encontrar, en esta tarea, **qué va a decidir el ejecutor si nadie se lo dice**.

Lo de abajo son lentes, no categorías. Se pasan todas por dentro y salen a la conversación solo las que devuelven algo. Una lente que no devuelve nada es gratis; una categoría que no se eligió es un punto ciego — por eso no hay tipos de tarea aquí.

Ninguna lista agota una tarea. Si al pensarla aparece algo que no calza en ninguna lente, ese hallazgo vale más que las siete juntas.

---

## Las lentes

### De dónde sale lo que es "correcto"

¿La verdad está en el ticket, en el código que ya existe, en un sistema que se está reemplazando, o en la cabeza de alguien?

Cuando la fuente es código existente, aparece la decisión más grande y menos visible: **sus defectos, ¿se replican o se corrigen?** El ejecutor va a deducir la regla leyendo, y si lo que lee es el defecto, deduce el defecto. Las dos respuestas son defendibles y opuestas, así que elegir en silencio es lo peor que puede pasar.

Cuando la fuente está en la cabeza de alguien y no escrita, probablemente haya que parar antes de escribir el prompt.

### Dónde termina

No qué hay que hacer, sino qué está cerca y no se toca. Con permiso de escritura, lo que no se excluye queda disponible.

Es la lente que más rinde y la que más se olvida, porque el ticket describe el centro de la tarea y nunca su borde.

### Quién más usa lo que se toca

Consumidores que el ticket no menciona porque para quien lo escribió eran obvios. Firmas, contratos, componentes compartidos, tablas leídas por otro proceso.

La pregunta útil no es "¿qué se modifica?" sino "¿qué se rompe si esto cambia de forma?".

### El camino que no es feliz

El ticket describe qué pasa cuando todo sale bien. Lo demás queda a criterio: sin datos, sin permiso, el otro sistema no responde, el valor viene nulo, la lista viene vacía.

Rinde cuando existe un afuera —usuarios, otro sistema, datos reales— y no rinde en trabajo puramente interno.

### Qué precedente existe y no está nombrado

¿Hay algo equivalente ya resuelto en el repositorio? Casi siempre sí, y casi nunca se dice.

Nombrarlo ahorra más que cualquier instrucción de estilo, porque el ejecutor deja de inventar un patrón propio. Si no existe precedente, eso también es un dato: el primero fija el patrón para los que vengan.

### Qué no se deshace

¿Qué parte no se arregla con otro prompt? Datos que ya corrieron, cambios que salieron a producción, integraciones que dispararon algo del otro lado.

Cuando esta lente devuelve algo, la verificación antes de mandar pesa más que en cualquier otra tarea, y conviene decirlo.

### Cómo se sabe que quedó

¿Podría verificarlo alguien que no estuvo en esta conversación? Si el criterio no se deja escribir, el problema es del ticket y no del prompt, y eso se dice ahora y no después de dos sesiones.

En trabajo donde el comportamiento observable no cambia — portar, reordenar, limpiar — esta lente es la más difícil y la más necesaria, porque "que funcione" no distingue el éxito del fracaso.

---

## Cómo se usan

**No son excluyentes.** Una tarea puede activar cuatro a la vez, y activar cuatro no la vuelve compleja: solo significa que hay cuatro decisiones que alguien va a tomar.

**No todas rinden siempre.** El filtro es el mismo del método: si no se puede nombrar qué protege una pregunta, no se hace. Preguntar por el camino de error en un cambio de texto de una etiqueta es ruido.

**Cuando dos lentes jalan a lados opuestos, se dice.** Portar pide preservar el comportamiento; mejorar pide cambiarlo. Si la tarea tiene las dos cosas adentro, ese conflicto es el encuadre — no se resuelve por dentro eligiendo la que parezca más razonable.

**Lo que ya está resuelto en el ticket no se vuelve a preguntar.** Un buen ticket contesta varias de estas solo. Repetirlas para demostrar rigor es la forma más rápida de que la persona deje de leer el encuadre.
