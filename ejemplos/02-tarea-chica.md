# Ejemplo 2 — Tarea chica

Contrapeso del ejemplo anterior. El encuadre no es un peaje: cuando la tarea no tiene bordes, se dice en una línea y se pasa al prompt.

Ticket inventado.

---

## La persona pega el ticket

> CLAVE-455 — Corregir el texto del botón de exportar
> Dice "Exportar Excel" y debe decir "Exportar a Excel" en las tres pantallas de reportes.

## El asistente encuadra

> Sin bordes: cambio de texto en tres lugares conocidos, sin lógica, reversible. Voy al prompt.

Eso es todo. Preguntar por el camino de error, por los consumidores o por el precedente sería ruido — no protegen nada aquí, y hacerlo enseña a la persona a saltarse el encuadre en las tareas donde sí importa.

## El prompt

```xml
<contexto>
Las tres pantallas de reportes del módulo de administración.
</contexto>

<tarea>
Cambia el texto del botón de exportación de "Exportar Excel" a "Exportar a Excel".
</tarea>

<alcance>
Solo el texto visible del botón. No toques la lógica de exportación ni los
nombres de archivo generados.
</alcance>

<criterio_de_aceptacion>
Las tres pantallas muestran el texto nuevo; la exportación sigue funcionando igual.
</criterio_de_aceptacion>
```

Cuatro bloques. `<rol>`, `<restricciones>` y `<formato_salida>` se sacaron porque no aportaban nada: rellenarlos habría alargado el prompt sin agregar una sola decisión.

## Vuelve la sesión

> Listo, las tres.

Se anota el resultado y se cierra. No hay nada que proponer.
