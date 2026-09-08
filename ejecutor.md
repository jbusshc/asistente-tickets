# El ejecutor

Quién recibe el prompt y qué trae puesto. Es el único archivo que cambia si cambias de agente de desarrollo; el método no se toca.

**Qué es:** plugin de desarrollo de la empresa, sobre Claude Code.

**Ve el repositorio:** sí. Abre, busca y navega archivos por su cuenta. En el prompt van rutas o un punto de entrada, no código pegado.

**Base de conocimiento:** sí, la consulta solo.

**Lineamientos de código:** los trae cargados. No se repiten en el prompt.

**Escribe en el repositorio:** sí. Por eso el alcance es la parte más importante del prompt: lo que no se excluye queda disponible.

**Cómo trabaja:** en sesión iterativa, con subagentes. Planifica solo — no se le entrega un plan, se le entrega un encuadre.

**Cómo vuelve el resultado:** cambios aplicados más el resumen de la sesión.

---

Una sesión completa es un intento, no cada mensaje dentro de ella.

Antes de dar algo por inexistente, corresponde pedirle que lo busque: alcanza más de lo que la persona revisó.
