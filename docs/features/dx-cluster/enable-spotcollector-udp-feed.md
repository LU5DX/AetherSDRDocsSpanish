# Activar la fuente UDP de SpotCollector

AetherSDR puede recibir spots DX transmitidos por SpotCollector de Ham Radio Deluxe a través de UDP y mostrarlos en el panadapter. Use esta página para iniciar el receptor y, opcionalmente, habilitarlo en cada arranque.

## Antes de comenzar

- Ham Radio Deluxe con SpotCollector debe estar en ejecución y configurado para transmitir datos de spots por UDP.
- Conozca en qué puerto UDP está transmitiendo SpotCollector y confirme que coincide con el que configuró en AetherSDR.

## Pasos

1. Abra `Settings > SpotHub...`.
2. Haga clic en la pestaña **SpotCollector**.
3. Establezca **UDP Port:** en el puerto en el que SpotCollector está transmitiendo. Rango válido: 1–65535. Este valor se guarda como `SpotCollectorPort`.
4. Haga clic en **Start**. El indicador de estado cambia a **Listening** cuando el socket UDP se enlaza correctamente.
5. Verifique que los datos entrantes aparezcan en la consola **SpotCollector Spots**.
6. Para iniciar el receptor automáticamente en cada arranque, habilite **Auto-start on startup**. Esto se guarda como `SpotCollectorAutoStart`.

## Qué hace cada control

| Control | Comportamiento | Clave de configuración | Rango válido |
|---|---|---|---|
| **UDP Port:** | Puerto UDP en el que AetherSDR escucha las transmisiones de SpotCollector. | `SpotCollectorPort` | 1–65535 |
| **Start / Stop** | Inicia o detiene el receptor UDP. | — | — |
| **Auto-start on startup** | Inicia el receptor automáticamente cuando AetherSDR se lanza. | `SpotCollectorAutoStart` | — |
| **SpotCollector Spots** | Consola de solo lectura que muestra los datos de spots recibidos. | — | — |

## Consejos

- Los spots recibidos de SpotCollector aparecen en la lista unificada de spots en la pestaña **Spot List**, junto con spots de otras fuentes. La columna **Source** los identifica.
- Si la superposición de spots en el panadapter no es visible, verifique que **Spots:** esté configurado como **Enabled** en la pestaña **Display**.

## Solución de problemas

- **El estado permanece en Stopped después de hacer clic en Start** — Es posible que otra aplicación ya esté enlazada al mismo puerto UDP. Cambie **UDP Port:** a un puerto libre y actualice SpotCollector para que coincida.
- **La consola SpotCollector Spots está vacía** — Confirme que SpotCollector esté en ejecución y configurado para transmitir en el mismo puerto UDP. Verifique que ningún cortafuegos esté bloqueando el tráfico UDP local en ese puerto.
- **Los spots no aparecen en el panadapter** — Abra la pestaña **Display** y confirme que **Spots:** esté en **Enabled**.

## Relacionado

- [Descripción general de SpotHub](overview.md)
- [Ajustar densidad, posición, tamaño de fuente y duración de los spots](tune-spot-density-position-font-size-and-lifetime.md)
- [Sintonizar un spot haciendo doble clic en la lista de spots](tune-to-a-spot-by-double-clicking-the-spot-list.md)
- [Elegir colores para cada fuente de spots](pick-colors-for-each-spot-source.md)
