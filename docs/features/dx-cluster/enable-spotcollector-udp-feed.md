# Habilitar el feed UDP de SpotCollector

AetherSDR puede recibir spots de DX transmitidos por SpotCollector de Ham Radio Deluxe mediante UDP y mostrarlos en su panadapter. Use esta página para iniciar el receptor y configurarlo para que se ejecute automáticamente al arrancar.

## Antes de comenzar

- SpotCollector debe estar configurado para transmitir datos de spots por UDP en un puerto de su elección.
- Tenga a mano el número de puerto UDP en el que SpotCollector está transmitiendo.

## Pasos

1. Haga clic en `Settings > SpotHub...` para abrir el diálogo SpotHub.
2. Haga clic en la pestaña **SpotCollector**.
3. Establezca **UDP Port:** en el puerto en el que SpotCollector está transmitiendo. Rango válido: 1–65535. Este valor se guarda como `SpotCollectorPort`.
4. Haga clic en **Start** para comenzar a escuchar. El indicador de estado cambia a **Listening** cuando el puerto está abierto.
5. Los spots entrantes aparecen en la consola **SpotCollector Spots** a medida que se reciben.
6. Para iniciar el receptor automáticamente cada vez que AetherSDR se inicia, habilite **Auto-start on startup**. Esto se guarda como `SpotCollectorAutoStart`.

## Qué hace cada control

| Control | Descripción | Clave de configuración |
|---|---|---|
| **UDP Port:** | Puerto UDP en el que SpotCollector transmite. Rango válido: 1–65535. | `SpotCollectorPort` |
| **Start / Stop** | Inicia o detiene el receptor UDP. | — |
| **Auto-start on startup** | Inicia el receptor automáticamente cuando AetherSDR se lanza. | `SpotCollectorAutoStart` |
| **SpotCollector Spots** | Consola de solo lectura que muestra los spots recibidos. | — |

## Consejos

- Los spots recibidos de SpotCollector aparecen en la pestaña unificada **Spot List** junto con los spots de todas las demás fuentes. La columna Source los identifica.
- Haga doble clic en cualquier fila de la Spot List para sintonizar su radio en esa frecuencia.

## Solución de problemas

- **El estado permanece en Stopped después de hacer clic en Start** — Verifique que el número de puerto UDP en AetherSDR coincida con el que SpotCollector está configurado para transmitir. Asegúrese de que ningún cortafuegos u otra aplicación esté bloqueando ese puerto.
- **No aparecen spots en la consola** — Confirme que SpotCollector esté transmitiendo activamente y que ambas aplicaciones estén ejecutándose en el mismo equipo, o que la transmisión llegue a la interfaz de red del equipo con AetherSDR.

## Relacionados

- [Descripción general de SpotHub](overview.md)
- [Sintonizar un spot haciendo doble clic en la lista de spots](tune-to-a-spot-by-double-clicking-the-spot-list.md)
- [Ajustar densidad, posición, tamaño de fuente y tiempo de vida de los spots](tune-spot-density-position-font-size-and-lifetime.md)
- [Elegir colores para cada fuente de spots](pick-colors-for-each-spot-source.md)
