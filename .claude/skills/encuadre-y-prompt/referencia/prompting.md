# Cómo se redacta el prompt

Basado en la guía de prompting de Anthropic:
`platform.claude.com/docs/en/build-with-claude/prompt-engineering/claude-prompting-best-practices`

Para el asistente, no para la persona.

---

## Los bloques

```xml
<rol>                    quién resuelve esto
<contexto>               dónde vive lo que se toca, y una frase de por qué
<tarea>                  qué hay que producir
<alcance>                qué entra y qué queda fuera
<restricciones>          con su motivo
<criterio_de_aceptacion> cómo se verifica
<formato_salida>         qué devuelve además del cambio
```

Etiquetar con XML reduce que se confunda instrucción con material. El contexto arriba y la instrucción abajo mejora la calidad de forma medible.

**No es un molde.** Un bloque que no aporta a esta tarea se saca. Siete bloques rellenados a la fuerza rinden menos que cuatro que dicen algo.

**`<contexto>` depende del ejecutor.** Con acceso al repositorio son rutas y puntos de entrada; pegar archivos que puede abrir solo llena el contexto sin agregar información, y lo pegado compite con la instrucción. Sin acceso, el código va pegado. Lo dice `ejecutor.md`; no se asume.

---

## Lo que más rinde

**Alcance explícito.** La primera cuando el ejecutor escribe en el repositorio. No basta decir qué hacer: hay que decir hasta dónde. "Refactorizó de paso el componente compartido" es el fallo más caro de deshacer.

**Criterio de aceptación que sirva para validar.** La persona valida después con esta misma lista, así que se escribe pensando en eso: casos concretos, no adjetivos. "Carga con un registro sin dirección" es verificable; "funciona correctamente" no.

**El motivo, no solo la regla.** El modelo generaliza desde la explicación a casos que la prohibición literal no cubría. "No toques el componente de tabla porque lo usan otras tres vistas" cubre los vecinos; sin el porqué, no.

**Verbo de acción.** Si el prompt dice "¿puedes sugerir cambios?", sugiere en vez de hacer. "Modifica", "Implementa", "Aplica". Cuando el resultado llegue como recomendaciones, revisar esto antes que nada.

**Verificar en vez de suponer.** Si el ejecutor tiene el repositorio, la instrucción correcta no es que pida lo que falta, es que lo busque:

> Verifica en el repositorio antes de asumir cómo funciona algo. Si algo no está ahí ni en lo que tengas accesible, dilo en vez de inventarlo.

**Frenar el trabajo de más.** Tiende a agregar abstracciones no pedidas, configurabilidad para escenarios que no existen, manejo defensivo de casos imposibles:

> Haz solo el cambio pedido. No refactorices código que no toca la tarea, no agregues configurabilidad que no se necesite hoy, y no documentes código que no cambiaste.

**No resolver contra los tests.** Cuando hay pruebas, a veces optimiza para que pasen en vez de resolver el problema:

> Implementa la lógica que resuelve el problema para todas las entradas válidas, no solo para los casos de prueba. Si algún test es incorrecto o la tarea es inviable, dilo en vez de rodearlo.

**Un ejemplo, si el formato de salida es particular.** Los ejemplos son de lo más fiable para dirigir formato y estructura. Uno basta en una tarea puntual; si hay un caso cerrado del mismo tipo en la bitácora, ahí está listo.

---

## Lo que estorba

**Los lineamientos que el ejecutor ya trae.** Repetirlos no los refuerza y agrega material que compite con la instrucción. Si no los aplicó, la reparación es nombrar la regla puntual, no cargar el manual.

**Escribirle el plan.** Si el ejecutor planifica solo, dictarle los pasos duplica trabajo y lo amarra a una descomposición peor que la suya. Los pasos numerados sirven cuando el orden importa de verdad.

**Mayúsculas y "DEBES".** Provocan sobreactivación y traen lo contrario de lo buscado.

**Auto-verificación pesada.** Los modelos recientes ya revisan su trabajo; forzarlo suma tiempo sin mejorar el resultado.

**Repetir una instrucción esperando que la segunda vez sí.** Si se ignoró, faltaba el motivo o faltaba peso. Repetir no da ninguno de los dos.

---

## Antes de entregarlo

- El verbo pide acción, no sugerencia
- El alcance dice qué queda fuera, con su motivo
- El criterio de aceptación lo puede verificar alguien que no estuvo en la conversación
- El contexto tiene la forma que corresponde al ejecutor
- No se repite lo que el ejecutor ya trae
- Está la línea de verificar en vez de suponer
- Está la línea de no hacer de más
- Ningún bloque está relleno solo por estar en la lista
