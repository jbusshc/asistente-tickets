# Ejemplo 1 — Portar un módulo

Muestra el encuadre haciendo su trabajo principal: sacar a la luz una decisión que el ticket delegaba en silencio.

Ticket inventado. Sirve para ver la forma de la conversación, no para copiar el contenido.

---

## La persona pega el ticket

> CLAVE-412 — Migrar el módulo de cobranza
> Portar el cálculo de cobranza a la plataforma nueva. El modelo de datos no cambia.

## El asistente encuadra

**Qué entiendo:** se reescribe el módulo de cobranza en la plataforma nueva conservando el comportamiento actual, sin tocar el esquema de datos.

**Qué va a decidir el ejecutor si no se lo decimos:**

- **De dónde saca lo correcto.** No hay especificación escrita: el sistema viejo es la verdad. Va a leer ese código y deducir la regla desde ahí. Eso trae la decisión grande: **si encuentra un defecto en el cálculo actual, ¿lo replica o lo corrige?** Las dos son defendibles, y si no lo decimos elige solo.
- **Cuánto reinterpreta.** La plataforma nueva tiene sus propios modismos. Sin decirlo, va a reescribir "como se hace ahora" en vez de portar comportamiento, y ahí es donde aparecen las diferencias sutiles.
- **Qué hace si el modelo de datos le queda incómodo.** Dijiste que no cambia, pero conviene que sea restricción y no dato de contexto: si le estorba, lo va a querer ajustar.

**Qué falta para verificar:** el comportamiento observable no cambia, así que "que funcione" no distingue éxito de fracaso. Hacen falta casos concretos con su resultado esperado, sacados del sistema viejo.

> **Supongo, corrígeme:** los defectos actuales se replican tal cual, porque hay procesos aguas abajo que ya dependen de ellos.

## La persona corrige

> Sí, se replican. Menos uno: hay un redondeo que en un caso da distinto y ya está reportado como bug aparte. Ese se replica igual, se arregla en su propio ticket.

## El asistente escribe el prompt

Lo guarda en `bitacora/CLAVE-412.md` para revisar antes de mandarlo.

```xml
<rol>
Desarrollador portando módulos de la plataforma anterior a la nueva en este repositorio.
</rol>

<contexto>
El módulo de cobranza actual es la especificación: no existe documento de
requerimientos, su comportamiento es la fuente de verdad.
Verifica en el repositorio antes de asumir cómo funciona algo. Si algo no
está ahí ni en la base de conocimiento, dilo en vez de inventarlo.
</contexto>

<tarea>
Porta el cálculo de cobranza a la plataforma nueva preservando el
comportamiento observable actual, caso por caso.
</tarea>

<alcance>
Entra: el módulo de cobranza y sus pruebas.
Queda fuera: el esquema de base de datos y el módulo de facturación, porque
hay procesos aguas abajo que dependen de ambos y no están en revisión.
</alcance>

<restricciones>
Preserva el comportamiento actual incluso donde parezca incorrecto. Hay un
redondeo que difiere en un caso y está reportado como bug aparte: replícalo
tal cual, porque corregirlo aquí desalinearía este módulo del resto.
El modelo de datos no cambia. Si algo del esquema estorba, dilo en vez de ajustarlo.
Porta comportamiento, no reinterpretes: usa los modismos de la plataforma nueva
solo donde no cambien resultados.
</restricciones>

<criterio_de_aceptacion>
- Los casos de cálculo del módulo viejo dan idéntico resultado en el nuevo,
  incluido el del redondeo divergente.
- El esquema de base de datos quedó sin cambios.
- El módulo de facturación no fue tocado.
</criterio_de_aceptacion>

<formato_salida>
Los cambios aplicados, más la lista de casos verificados con su resultado
en ambas versiones.
</formato_salida>
```

## Vuelve la sesión

> Portó todo bien pero me "arregló" el redondeo. Quedó distinto al viejo.

**Diagnóstico:** resolvió un problema distinto del que se pidió. La instrucción estaba, pero enterrada en un bloque de restricciones largo, donde compite con las demás. → Subirle peso: la paridad de comportamiento pasa a ser lo primero del bloque, con el motivo delante.

Sesión 2 con ese cambio: cerrada.
