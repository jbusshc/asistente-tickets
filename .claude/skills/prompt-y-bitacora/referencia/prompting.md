# Cómo se escribe el prompt

Basado en la guía de prompting de Anthropic:
`platform.claude.com/docs/en/build-with-claude/prompt-engineering/claude-prompting-best-practices`

Leer esto antes de redactar. Es para el asistente, no para la persona.

---

## Los bloques y su orden

```xml
<rol>          quién resuelve esto
<estandares>   las reglas que aplican a este cambio
<material>     lo que se toca y lo que define su contrato
<ejemplo>      opcional — ver más abajo
<tarea>        qué hay que producir
<restricciones> con su motivo
<formato_salida> qué debe volver
```

El material va **antes** de la tarea. Colocar los datos largos arriba y la consulta al final mejora la calidad de forma medible; en pruebas con entradas complejas la diferencia llegó a 30%. Etiquetar cada bloque con XML reduce que se confunda instrucción con material.

Si hay varios documentos, anidar: cada uno en `<documento>` con su `<fuente>` dentro.

---

## Las palancas que más rinden

**Dar el motivo, no solo la regla.** El modelo generaliza desde la explicación a casos que la prohibición literal no cubría. "No uses puntos suspensivos porque esto lo lee un motor de texto a voz que no sabe pronunciarlos" funciona mejor que la prohibición sola, y cubre los casos vecinos.

**Decir qué hacer, no qué no hacer.** "Devuelve el código modificado y una lista de riesgos" supera a enumerar todo lo que no debe aparecer. Ocupa menos y es más robusto.

**Verbo de acción explícito.** Esta es la que más se pasa por alto. Si el prompt dice "¿puedes sugerir cambios para mejorar esta función?", el modelo sugiere en vez de hacer. Para que actúe hay que escribirlo directo: "Modifica esta función para..." o "Aplica estos cambios a...". Cuando el resultado llegue como recomendaciones en vez de código, revisar esto antes que nada.

**Ejemplos, cuando valen la pena.** Anthropic los señala como de lo más fiable para dirigir formato, tono y estructura, y recomienda de tres a cinco, envueltos en `<ejemplo>` dentro de `<ejemplos>`, relevantes al caso real y variados entre sí.

Ahora bien, en una tarea puntual producir tres ejemplos cuesta más de lo que rinde. Criterio práctico: **un ejemplo cuando el formato de salida es particular o cuando el mismo tipo de tarea se repite.** Si es un cambio único y el formato es obvio, saltarlo. Si ya hay un caso resuelto de ese tipo en la bitácora, ahí está el ejemplo listo.

**No especular sobre lo que no vio.** Cuando se entrega contexto mínimo — que es lo correcto — el modelo puede rellenar con suposiciones sobre archivos que no recibió. Vale una línea explícita:

> No hagas afirmaciones sobre código que no está en este contexto. Si necesitas algo que no te di, pídelo.

Esta instrucción es el complemento natural del contexto mínimo: se le da poco, y se le dice qué hacer cuando falte.

**Frenar la sobreingeniería.** El modelo tiende a agregar de más: archivos extra, abstracciones no pedidas, flexibilidad para escenarios hipotéticos, manejo defensivo de casos que no pueden ocurrir. Una línea alcanza como base:

> Haz solo el cambio pedido. No refactorices código que no toca la tarea, no agregues configurabilidad ni abstracciones que no se necesiten hoy, y no documentes código que no cambiaste.

Si el problema aparece igual, ampliarlo por eje concreto: alcance, documentación, código defensivo, abstracciones.

**No resolver contra los tests.** Cuando hay pruebas de por medio, el modelo a veces optimiza para que pasen en vez de resolver el problema. Si se detecta:

> Implementa la lógica que resuelve el problema para todas las entradas válidas, no solo para los casos de prueba. Si algún test es incorrecto o la tarea es inviable, dilo en vez de rodearlo.

---

## Lo que ya no hace falta y estorba

**Mayúsculas y "DEBES".** Los modelos actuales responden más al prompt que las generaciones anteriores. Donde antes se escribía "CRÍTICO: DEBES usar esta herramienta", hoy basta "Usa esta herramienta cuando...". El énfasis agresivo provoca sobreactivación y trae lo contrario de lo buscado.

**Pasos prescriptivos para el razonamiento.** Una instrucción general como "analiza esto a fondo" suele producir mejor razonamiento que un plan paso a paso escrito a mano. Los pasos numerados sirven para procedimientos donde el orden importa de verdad, no para pensar.

**Instrucciones pesadas de auto-verificación.** Pedir que revise su trabajo contra los criterios ayuda en modelos más antiguos. Los recientes ya lo hacen solos, y forzarlo agrega tiempo sin mejorar el resultado. Si se nota que verifica de más, quitar esas líneas en vez de reescribirlas.

**Repetir la instrucción esperando que la segunda vez sí.** Si algo se ignoró, faltaba la información o faltaba el motivo. Repetir no lo agrega.

---

## Para tareas de análisis sobre documentos

Cuando el trabajo es leer y documentar en vez de modificar código, hay una técnica extra: pedir que cite primero los fragmentos relevantes del material y después haga el análisis. Ayuda a que se ancle en lo que efectivamente dice la fuente en vez de en lo que suena razonable, y de paso deja verificable de dónde salió cada afirmación.

---

## Comprobación antes de entregar el prompt

- El verbo de la tarea pide acción, no sugerencia
- Cada restricción trae su motivo
- Está la línea de no especular sobre lo que no recibió
- Está la línea de no hacer de más, si es cambio de código
- El formato de salida está fijado
- Nada en mayúsculas ni "DEBES"
- El material va antes de la tarea
