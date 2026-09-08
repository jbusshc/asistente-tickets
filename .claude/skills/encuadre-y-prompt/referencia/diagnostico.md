# Diagnóstico

Para el asistente. La persona escribe en prosa lo que vio; la clasificación es interna.

La pregunta que ordena todo: **¿existe en algún lado lo que faltó?** Si existe y no se usó, se repara el prompt. Si no existe, ningún prompt lo invoca y hay que parar.

Lo de abajo son causas frecuentes, no un árbol de decisión. Si lo observado no calza en ninguna, describir la causa real vale más que forzar la que más se le parezca.

Una sesión completa es un intento.

---

## Se repara el prompt

**Tocó lo que no debía.** Modificó algo cercano que no era parte de la tarea. Con permiso de escritura es el fallo más caro. → Alcance explícito con su motivo, y con peso propio: una exclusión perdida al final de un bloque largo se lee como nota al pie.

**Leyó de más.** Se paseó por el proyecto, se llenó de contexto y el resultado salió genérico o incompleto. → Delimitar dónde mirar y dar un punto de entrada. Sospechar de esto siempre que el prompt haya crecido entre sesiones y el resultado haya empeorado.

**Ignoró una regla que sí tenía.** El lineamiento existe y el ejecutor lo trae cargado, pero no lo aplicó. → No se repara entregándolo de nuevo: se nombra esa regla puntual para subirle peso. Si se señaló y volvió a ignorarla, sospechar de tarea demasiado grande.

**No encontró lo que se le nombró.** Ruta mala, archivo movido, buscó donde no era. → Verificar la referencia antes de reescribir nada. Es el más barato de arreglar y el que más se confunde con otros.

**Faltó una restricción.** Hizo algo razonable pero indeseado: cambió una interfaz, fijó un valor a mano, arregló de paso lo que nadie tocó. → Restricción con su motivo.

**Resolvió un problema distinto del que se pidió.** Fue a la raíz cuando se quería el síntoma, o al revés. Preservó cuando se quería mejorar, o mejoró cuando se quería preservar. → Decir explícitamente cuál de los dos, porque ambos son defendibles.

**Objetivo ambiguo.** El resultado es defendible pero no era lo buscado, y cuesta explicar por qué está mal. → Reescribir la tarea en imperativo con el resultado observable. Segunda vez en la misma tarea: tratarlo como requerimiento mal definido y parar.

**Formato no fijado.** Contenido correcto, estructura distinta. → Fijar la estructura al final del prompt.

**Sugirió en vez de hacer.** Devolvió recomendaciones donde se esperaba el trabajo. → El verbo pedía opinión.

**Hizo de más.** Abstracciones o configurabilidad para escenarios que no existen. → Línea explícita de alcance.

**Faltó algo que sí existe.** Antes de agregarlo al prompt, revisar si bastaba con decirle dónde buscarlo. Cargar el prompt con lo que puede leer solo es la forma más común de inflarlo.

---

## Se para

**No existe en ninguna parte accesible.** Un prompt que lo invente produce algo que aparenta cumplir lo inexistente, peor que el fallo porque pasa desapercibido.

**No existe el formato o la plantilla de salida.** Puede trabajarse libre y anotarlo, pero si el caso se repite hay que pedirlo.

**Excede lo que el ejecutor puede hacer.** Le falta una capacidad o un acceso. Suele ser información de estado, no un defecto.

**El requerimiento está mal definido.** Pide algo contradictorio o incompleto. Se nota porque el criterio de aceptación no se deja escribir. → Aclararlo con quien lo originó. Lo más barato de detectar temprano y lo que más cuesta admitir, porque obliga a volver sobre alguien.

Antes de clasificar aquí, pedir que el ejecutor busque. Marcar "no existe" algo que sí existía escala un caso que no correspondía.

---

## Señales que confunden

**Inventó datos.** Casi siempre el prompt dio permiso implícito: un "completa lo que falte", o un formato que exigía un campo sin fuente. Revisar el prompt antes de culpar al ejecutor.

**Preguntó en vez de entregar.** No es fallo, es la conducta correcta ante un vacío real. Decidir si la respuesta existe (se le dice dónde) o no (se para).

**Cumplió el criterio y aun así no sirve.** El criterio estaba incompleto. Es un hallazgo sobre cómo se definió "listo", no sobre el prompt. Se repite más que ningún otro.

**El resumen de la sesión dice que quedó y no quedó.** El ejecutor reporta lo que intentó, no lo que se verificó. Vale como pista, no como evidencia.

**Funcionó la vez pasada y ahora no.** Sospechar del alcance antes que de la instrucción: lo que suele haber cambiado es cuánto terreno tenía disponible.

**No hay con qué diagnosticar.** Decirlo en vez de elegir la causa más probable. Pedir dos cosas: qué se esperaba y qué llegó.
