# Comprobar las tasas de datos por categoría (Audio, FFT, Waterfall, Meters, DAX)

El cuadro de diálogo Network Diagnostics muestra las tasas de ingreso en vivo para cada categoría de flujo — Audio, FFT, Waterfall, Meters y DAX — actualizadas cada segundo. Úselo para confirmar que cada flujo está entregando datos a la tasa esperada e identificar qué categoría consume ancho de banda o está perdiendo paquetes.

## Antes de comenzar

- AetherSDR debe estar en ejecución. El cuadro de diálogo se abre esté o no conectada una radio, pero los valores de tasa solo son significativos cuando hay conexión.

## Pasos

1. Haga clic en `Settings > Network...`.
2. Haga clic en la pestaña **Details**.
3. Localice el grupo **Incoming Stream Rates** en el lado derecho de la pestaña.
4. Lea los indicadores de tasa por categoría: **Audio**, **FFT**, **Waterfall**, **Meters** y **DAX**. Cada uno muestra la tasa de ingreso actual en kbps, recalculada una vez por segundo.
5. Localice el grupo **Packet Loss** debajo de la columna izquierda.
6. Lea los indicadores de pérdida correspondientes: **Audio**, **FFT**, **Waterfall**, **Meters** y **DAX**. Cada uno muestra paquetes perdidos, paquetes totales y un porcentaje de pérdida en el formato `errores / total (pct%)`.
7. Para ver una vista de serie temporal de las tasas de bits por flujo, haga clic en la pestaña **Rates**. Use el selector **Timeframe** en la esquina superior derecha de la barra de pestañas para elegir qué tan atrás muestra el historial el gráfico.
8. Para ver una vista de serie temporal de la pérdida de paquetes por categoría de flujo, haga clic en la pestaña **Packet Loss**.
9. Cuando termine, haga clic en **Close**.

## Qué hace cada control

| Control / Indicador       | Ubicación / Grupo                 | Significado                                                                                                                                                      |
|---------------------------|-----------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Overview** (pestaña)    | Barra de pestañas                 | Muestra cuatro tarjetas de estado (Status, Latency, Packet Loss, Audio Buffer) y cuatro gráficos de serie temporal (Latency and Jitter, Recent Packet Loss, Total Stream Rates, Audio Buffer). |
| **Details** (pestaña)     | Barra de pestañas                 | Cuadrícula desplazable con valores etiquetados para los grupos Network Status, Incoming Stream Rates, Packet Loss y Audio Playback.                                |
| **Latency** (pestaña)     | Barra de pestañas                 | Gráfico de serie temporal de ancho completo de RTT, brecha de llegada y jitter en ms.                                                                             |
| **Rates** (pestaña)       | Barra de pestañas                 | Gráfico de serie temporal de ancho completo con escala logarítmica de las tasas de bits entrantes por flujo (RX total, Audio, FFT, Waterfall, Meters, DAX) en kbps. |
| **Packet Loss** (pestaña) | Barra de pestañas                 | Gráfico de serie temporal de ancho completo del porcentaje de pérdida de paquetes por categoría de flujo.                                                        |
| **Audio** (pestaña)       | Barra de pestañas                 | Gráfico de serie temporal de ancho completo del llenado del búfer de reproducción (ms) y subejecuciones/s.                                                       |
| **Logs** (pestaña)        | Barra de pestañas                 | Visualización en vivo del archivo de registro de AetherSDR, filtrado por casillas de verificación de categoría. Resaltado de sintaxis por nivel de registro y nombre de categoría. El selector **Timeframe** está oculto mientras esta pestaña está activa. |
| **Timeframe**             | Esquina superior derecha de la barra de pestañas | Selecciona qué tan atrás muestran el historial los gráficos de serie temporal. El valor predeterminado es **5 minutes**. Opciones: 1 minute, 5 minutes, 15 minutes, 1 hour, 1 day, 1 week. Oculto cuando la pestaña **Logs** está activa. |
| **Audio** (tasa)          | Details > Incoming Stream Rates   | Tasa de ingreso para el flujo de audio del receptor, en kbps.                                                                                                    |
| **FFT** (tasa)            | Details > Incoming Stream Rates   | Tasa de ingreso para los datos FFT del panadapter, en kbps.                                                                                                      |
| **Waterfall** (tasa)      | Details > Incoming Stream Rates   | Tasa de ingreso para los datos del waterfall, en kbps.                                                                                                           |
| **Meters** (tasa)         | Details > Incoming Stream Rates   | Tasa de ingreso para los datos de los medidores, en kbps.                                                                                                        |
| **DAX** (tasa)            | Details > Incoming Stream Rates   | Tasa de ingreso para los datos de audio DAX, en kbps.                                                                                                            |
| **Total RX**              | Details > Incoming Stream Rates   | Tasa de recepción agregada en todas las categorías de flujo, en kbps.                                                                                            |
| **Total TX**              | Details > Incoming Stream Rates   | Tasa de transmisión agregada, en kbps.                                                                                                                           |
| **Audio** (pérdidas)      | Details > Packet Loss             | Paquetes de audio perdidos frente al total, con porcentaje de pérdida.                                                                                           |
| **FFT** (pérdidas)        | Details > Packet Loss             | Paquetes FFT perdidos frente al total, con porcentaje de pérdida.                                                                                                |
| **Waterfall** (pérdidas)  | Details > Packet Loss             | Paquetes de waterfall perdidos frente al total, con porcentaje de pérdida.                                                                                       |
| **Meters** (pérdidas)     | Details > Packet Loss             | Paquetes de medidores perdidos frente al total, con porcentaje de pérdida.                                                                                       |
| **DAX** (pérdidas)        | Details > Packet Loss             | Paquetes DAX perdidos frente al total, con porcentaje de pérdida.                                                                                                |
| **Filter Categories**     | Pestaña Logs                      | Casillas de verificación por categoría que filtran la vista del registro. Incluye una categoría General (predeterminada) más todas las categorías registradas de LogManager. |
| **Select All**            | Pestaña Logs                      | Muestra todas las categorías de registro en el visor.                                                                                                            |
| **Deselect All**          | Pestaña Logs                      | Oculta todas las categorías de registro del visor.                                                                                                               |
| **Live / Paused**         | Pestaña Logs                      | Cuando está en Live, el visor se desplaza automáticamente a la salida más reciente. Desplazarse hacia arriba pausa automáticamente; hacer clic en Live reanuda y salta al final. |
| **Close**                 | Parte inferior del cuadro de diálogo | Cierra el cuadro de diálogo.                                                                                                                                     |

Todos los valores de tasa se calculan a partir del delta del recuento de bytes en el intervalo de un segundo anterior y se expresan en kbps. Los recuentos de pérdidas se infieren de los números de secuencia VITA-49 faltantes.

## Pestaña Logs

La pestaña **Logs** sigue el archivo de registro de AetherSDR en tiempo real. La ruta completa del archivo que se está siguiendo se muestra en la etiqueta de ruta de registro en la parte superior de la pestaña.

La salida del registro tiene resaltado de sintaxis por nivel de registro y nombre de categoría:

- Las marcas de tiempo se muestran en gris azulado tenue.
- Las entradas `DBG` se muestran en gris azulado tenue.
- Las entradas `INF` se muestran en azul claro.
- Las entradas `WRN` se muestran en ámbar.
- Las entradas `CRT` y `FTL` se muestran en rojo.
- Los nombres de categoría se muestran en gris claro negrita.
- Los valores numéricos y los tokens de protocolo (por ejemplo, `UDP`, `TCP`, `VITA-49`, `RX`, `TX`) se muestran en colores de acento distintivos.

Use las casillas de verificación **Filter Categories** para mostrar solo las categorías relevantes para el problema que está diagnosticando. Haga clic en **Select All** para restaurar todas las categorías, o en **Deselect All** para limpiar la vista antes de seleccionar categorías específicas. Desplácese hacia arriba para pausar el desplazamiento automático; haga clic en **Live** para reanudar y saltar al final.

## Consejos

- Una tasa de 0 kbps para una categoría que debería estar activa (por ejemplo, **Audio** mientras hay un slice abierto) indica que el flujo ha dejado de llegar. Verifique primero el indicador **Status** en el grupo **Network Status** de la pestaña **Details**.
- Grandes variaciones en la tasa de una categoría de un segundo a otro pueden indicar entrega por ráfagas incluso cuando el recuento de pérdidas permanece en cero.
- Cero pérdidas en el grupo **Packet Loss** no descarta fluctuación o ráfagas que llegan tarde. Si el audio se entrecorta pero las pérdidas muestran cero, verifique el grupo **Audio Playback** en la pestaña **Details** para detectar subejecuciones y fluctuación, o revise la pestaña **Audio** para ver una serie temporal del llenado del búfer y subejecuciones/s.
- La pestaña **Rates** usa un eje y logarítmico, lo que facilita ver flujos de baja tasa (por ejemplo, Meters) junto con flujos de alta tasa (por ejemplo, RX total) en el mismo gráfico.
- Amplíe el selector **Timeframe** a **1 hour** o más cuando investigue problemas intermitentes que ocurren con poca frecuencia.

## Solución de problemas

- **Todas las tasas de categoría muestran 0 kbps** — La radio no está transmitiendo. Confirme que la conexión esté activa verificando **Status** y **Target Radio IP** en el grupo **Network Status** de la pestaña **Details**. Vuelva a conectar mediante `Settings > Connect to Radio...` si es necesario.
- **La tasa de DAX muestra 0 kbps cuando se espera DAX** — Es posible que la transmisión DAX no esté habilitada. Verifique que DAX esté iniciado; en plataformas compatibles, revise `Settings > Autostart DAX with AetherSDR`.
- **El porcentaje de pérdida no es cero en una sola categoría** — La pérdida está aislada en ese flujo. Esto puede indicar que la radio está sobrecargada para ese tipo de datos específico o que una cola de red está descartando preferentemente paquetes UDP de ese tamaño.
- **La pestaña Logs no muestra salida** — Confirme que la etiqueta de ruta de registro muestre una ruta de archivo válida. Si la ruta falta o el archivo no existe, reinicie AetherSDR y vuelva a abrir el cuadro de diálogo.

## Relacionado

- [Network Diagnostics overview](overview.md)
- [Measure RTT and packet drops during audio problems](measure-rtt-and-packet-drops-during-audio-problems.md)
- [Diagnose audio underruns and jitter](../../troubleshooting/networkdiagnostics/diagnose-audio-underruns-and-jitter.md)
- [Verify the radio's IP and local bind address](verify-the-radio-s-ip-and-local-bind-address.md)
