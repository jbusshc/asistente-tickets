# Diagnóstico de fallos

Para uso del asistente. La persona escribe en prosa lo que vio; la clasificación no se le pide.

La pregunta que ordena todo: **¿existe en algún lado la información que falta?** Si existe y no llegó, se repara el prompt. Si no existe, ningún prompt la invoca y hay que parar.

---

## Se repara el prompt

**Faltó información que sí existe.** Correcto en su lógica pero ignora una convención o un dato disponible. → Incorporarlo. Repetir "hazlo bien" no es la reparación.

**Sobró material.** Mezcla asuntos que no venían al caso, toca cosas que nadie pidió, o sale genérico pese a habérsele dado mucho. → Recortar. Empezar por aquí siempre que se haya entregado un archivo completo o varios documentos "por si acaso", y siempre que el prompt haya crecido entre intentos y el resultado haya empeorado.

**Faltó una restricción.** Hace algo razonable pero indeseado: cambia una interfaz, fija un valor a mano, arregla de paso lo que nadie tocó. → Restricción con su motivo; la razón cubre los casos vecinos que la prohibición literal no alcanza.

**Formato no fijado.** Contenido correcto, estructura distinta a la esperada, o cada ejecución entrega algo diferente. → Fijar la estructura al final del prompt.

**Tarea demasiado grande.** Cubre bien el principio y se degrada al final; o abarca varias piezas y ninguna queda completa. → Descomponer. Señal fuerte: dos intentos que fallan por causas distintas cada vez.

**Objetivo ambiguo.** El resultado es defendible pero no era lo buscado, y cuesta explicar por qué está mal. → Reescribir la tarea en imperativo con el resultado observable. Si no sale, el criterio de aceptación estaba flojo; si es la segunda vez en la misma tarea, tratarlo como requerimiento mal definido y parar.

**Sugirió en vez de hacer.** Devolvió recomendaciones, un plan o un análisis donde se esperaba el trabajo hecho. → El verbo de la tarea pedía opinión. "Modifica", "aplica", "reescribe" — no "puedes sugerir", "qué te parece si", "propón".

**Hizo de más.** Refactorizó lo que nadie pidió, agregó abstracciones o configurabilidad para escenarios que no existen, documentó código que no tocó. → Línea explícita de alcance: solo el cambio pedido, sin mejoras no solicitadas.

**Habló de código que no recibió.** Afirmó cosas sobre archivos que no estaban en el contexto. Es el riesgo natural de entregar contexto mínimo, y su reparación no es entregar más. → Decirle que no especule sobre lo que no tiene y que pida lo que le falte.

---

## Se para

**La información no existe documentada.** Se busca el dato o la regla y no está en ninguna parte accesible. Un prompt que la invente produce algo que aparenta cumplir lo inexistente, que es peor que el fallo porque pasa desapercibido.

**No existe el estándar o la plantilla.** El resultado debería seguir un formato que nadie definió. Puede trabajarse libre y anotarlo, pero si el caso se repite hay que pedirlo.

**La tarea excede lo que el sistema hace.** Requiere una capacidad que el ejecutor no tiene. Suele ser información de estado, no un defecto: registrarlo y buscar otra vía.

**El requerimiento está mal definido.** El ticket pide algo contradictorio o incompleto. Se nota porque el criterio de aceptación no se deja escribir. → Aclararlo con quien lo originó. Es lo más barato de detectar temprano y lo que más cuesta admitir, porque obliga a volver sobre alguien.

Antes de clasificar aquí, preguntar dónde buscó. Marcar "no existe" algo que sí existía escala un caso que no correspondía; marcar "falta contexto" algo que no existe quema intentos hasta agotarlos.

---

## Señales que confunden

**Inventó datos.** Casi siempre el prompt le dio permiso implícito: un "completa lo que falte", o un formato que exigía un campo sin fuente. Revisar el prompt antes de culpar al ejecutor.

**Preguntó en vez de entregar.** No es fallo, es la conducta correcta ante un vacío. Decidir si la respuesta existe (se agrega) o no existe (se para).

**Cumplió el criterio y aun así no sirve.** El criterio estaba incompleto. Es un hallazgo sobre cómo se definió "listo", no sobre el prompt. Anotarlo: se repite más que ningún otro.

**Funcionó la vez pasada y ahora no.** Sospechar de exceso de material antes que de nada: lo que suele haber cambiado es el volumen, no la instrucción.

**No hay con qué diagnosticar.** Resultado válido, y hay que decirlo en vez de elegir la causa más probable. Pedir solo dos cosas: qué se esperaba y qué llegó.
