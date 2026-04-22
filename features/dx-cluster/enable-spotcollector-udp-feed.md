# Activar la alimentación UDP de SpotCollector

AetherSDR puede recibir spots de DX transmitidos por SpotCollector de Ham Radio Deluxe a través de UDP y mostrarlos en el panadapter. Esta página explica cómo iniciar el receptor y configurarlo para que se ejecute automáticamente al arrancar.

## Antes de comenzar

- Ham Radio Deluxe con SpotCollector debe estar en ejecución en su red y configurado para transmitir datos de spots por UDP.
- Anote el puerto UDP en el que SpotCollector está transmitiendo. Deberá introducir ese puerto en AetherSDR.

## Pasos

1. Abra `Settings > SpotHub...`.
2. Haga clic en la pestaña **SpotCollector**.
3. Establezca **UDP Port:** en el puerto en el que SpotCollector está transmitiendo. Rango válido: 1–65535. Este valor se guarda como `SpotCollectorPort`.
4. Haga clic en **Start**. El indicador de estado cambia a **Listening** cuando el receptor está activo.
5. Confirme que los spots aparecen en la consola **SpotCollector Spots**.
6. Para iniciar el receptor automáticamente cada vez que AetherSDR arranque, active **Auto-start on startup**. Esto se guarda como `SpotCollectorAutoStart`.

## Qué hace cada control

| Control | Descripción | Clave de configuración |
|---|---|---|
| **UDP Port:** | Puerto UDP en el que AetherSDR escucha las transmisiones de SpotCollector. Rango válido: 1–65535. | `SpotCollectorPort` |
| **Start / Stop** | Inicia o detiene el receptor UDP. | — |
| **Auto-start on startup** | Inicia el receptor automáticamente cuando AetherSDR arranca. | `SpotCollectorAutoStart` |
| **SpotCollector Spots** | Consola de solo lectura que muestra los spots recibidos a medida que llegan. | — |

## Consejos

- Los spots de SpotCollector aparecen junto a los spots de otras fuentes en la pestaña **Spot List** y en el panadapter. Para controlar su apariencia en el panadapter, consulte [Elegir colores para cada fuente de spots](pick-colors-for-each-spot-source.md).
- Haga doble clic en cualquier fila de la pestaña **Spot List** para sintonizar el VFO a la frecuencia de ese spot.

## Solución de problemas

- **El estado permanece en Stopped después de hacer clic en Start** — Verifique que ninguna otra aplicación esté ya vinculada al mismo puerto UDP en esta máquina.
- **Los spots no aparecen en la consola** — Confirme que SpotCollector está configurado para transmitir al mismo puerto UDP y que el cortafuegos del equipo permite el tráfico UDP entrante en ese puerto.

## Relacionado

- [Descripción general de SpotHub](overview.md)
- [Ajustar densidad, posición, tamaño de fuente y duración de los spots](tune-spot-density-position-font-size-and-lifetime.md)
- [Elegir colores para cada fuente de spots](pick-colors-for-each-spot-source.md)
- [Sintonizar un spot haciendo doble clic en la lista de spots](tune-to-a-spot-by-double-clicking-the-spot-list.md)
