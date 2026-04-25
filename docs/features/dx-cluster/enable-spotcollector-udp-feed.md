# Habilitar el feed UDP de SpotCollector

AetherSDR puede recibir spots de DX transmitidos por SpotCollector de Ham Radio Deluxe mediante UDP y mostrarlos en el panadapter. Esta página explica cómo iniciar el receptor, configurar el puerto correcto y habilitarlo para que arranque automáticamente.

## Antes de comenzar

- SpotCollector debe estar instalado, configurado y en ejecución en la misma máquina o en la red local, y configurado para transmitir spots por UDP.
- Anote el puerto UDP en el que SpotCollector está transmitiendo — deberá ingresarlo en AetherSDR.

## Pasos

1. Abra `Settings > SpotHub...`.
2. Haga clic en la pestaña **SpotCollector**.
3. Configure **UDP Port:** con el puerto en el que SpotCollector está transmitiendo. Rango válido: 1–65535. Este valor se guarda como `SpotCollectorPort`.
4. Haga clic en **Start**.
5. Confirme que el indicador de estado cambia a **Listening**. Los spots entrantes aparecerán en la consola **SpotCollector Spots** a medida que lleguen.
6. Para que el receptor inicie automáticamente cada vez que AetherSDR se ejecute, habilite **Auto-start on startup**. Esto se guarda como `SpotCollectorAutoStart`.

## Qué hace cada control

| Control | Descripción | Clave de configuración |
|---|---|---|
| **UDP Port:** | Puerto UDP en el que AetherSDR escucha las transmisiones de SpotCollector. Rango válido: 1–65535. | `SpotCollectorPort` |
| **Start / Stop** | Inicia o detiene el receptor UDP. | — |
| **Auto-start on startup** | Inicia el receptor automáticamente al arrancar. | `SpotCollectorAutoStart` |
| **SpotCollector Spots** | Consola de solo lectura que muestra los spots recibidos de SpotCollector. | — |

## Consejos

- Los spots recibidos de SpotCollector aparecen junto a los spots de otras fuentes en la pestaña **Spot List**. La columna **Source** los identifica.
- Si la capa de spots del panadapter no es visible, verifique que **Spots:** esté configurado en **Enabled** en la pestaña **Display**.

## Solución de problemas

- **El estado permanece en Stopped o no aparecen spots** — Verifique que SpotCollector esté transmitiendo activamente y que el puerto UDP en AetherSDR coincida con el puerto configurado en SpotCollector. Compruebe que ningún cortafuegos esté bloqueando el tráfico UDP en ese puerto.
- **El receptor inicia pero el panadapter no muestra spots** — Confirme que la capa de spots principal esté activa: abra la pestaña **Display** y verifique que **Spots:** esté en **Enabled**.

## Relacionados

- [Descripción general de SpotHub](overview.md)
- [Ajustar densidad, posición, tamaño de fuente y duración de los spots](tune-spot-density-position-font-size-and-lifetime.md)
- [Elegir colores para cada fuente de spots](pick-colors-for-each-spot-source.md)
- [Sintonizar un spot haciendo doble clic en la lista de spots](tune-to-a-spot-by-double-clicking-the-spot-list.md)
- [Borrar todos los spots del panadapter](clear-all-spots-from-the-panadapter.md)
