# Diálogo de Diagnóstico de Red

Utilice esta página para monitorear el enlace de red en vivo entre AetherSDR y su FLEX-8600, confirmar las direcciones de conexión, inspeccionar las tasas de datos por flujo y revisar la salida del registro filtrada.

## Antes de comenzar

- AetherSDR debe estar ejecutándose. El diálogo no requiere una conexión activa con la radio, pero la mayoría de los campos y gráficos mostrarán valores significativos solo después de que se haya intentado una conexión.

## Abrir el diálogo

1. Haga clic en `Settings > Network...`.
2. Se abre el diálogo **Network Diagnostics**. Por defecto, muestra la pestaña **Overview**.

## Resumen de pestañas

El diálogo está organizado en siete pestañas. Seleccione la pestaña que coincida con lo que desea inspeccionar.

| Pestaña            | Qué muestra                                                                                                                                                |
|--------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Overview**       | Cuatro tarjetas de estado (Status, Latency, Packet Loss, Audio Buffer) y cuatro gráficos de series temporales (Latency y Jitter, Recent Packet Loss, Total Stream Rates, Audio Buffer). |
| **Details**        | Cuadrícula desplazable con valores etiquetados para los grupos Network Status, Incoming Stream Rates, Packet Loss y Audio Playback.                          |
| **Latency**        | Gráfico de series temporales a ancho completo de RTT, intervalo de llegada y jitter en ms.                                                                  |
| **Rates**          | Gráfico de series temporales a ancho completo con escala logarítmica de las tasas de bits entrantes por flujo (RX total, Audio, FFT, Waterfall, Meters, DAX) en kbps. |
| **Packet Loss**    | Gráfico de series temporales a ancho completo del % de pérdida de paquetes por categoría de flujo.                                                          |
| **Audio**          | Gráfico de series temporales a ancho completo del llenado del búfer de reproducción (ms) y subejecuciones/s. Incluye diagnósticos de audio RX por flujo que muestran la tasa de alimentación, el déficit, los paquetes tardíos, el código de clase de paquete y la salud del flujo para cada flujo de audio activo. |
| **Logs**           | Seguimiento en vivo del archivo de registro de AetherSDR, filtrado por casillas de verificación de categoría. Resaltado de sintaxis por nivel de registro y nombre de categoría. |

## Verificar la IP de la radio y la dirección de enlace local

1. Abra el diálogo **Network Diagnostics** como se describió anteriormente.
2. Seleccione la pestaña **Details**.
3. Localice el grupo **Network Status**.
4. Lea **Target Radio IP** — muestra la dirección IP de la radio a la que se conectó AetherSDR. Si no se ha realizado ninguna conexión, el campo muestra `Not connected`.
5. Lea **Selected Source** — muestra la interfaz de red local o la ruta de enlace que utilizó AetherSDR para llegar a la radio.
6. Lea **Local TCP** y **Local UDP** para ver los puntos finales locales exactos para cada protocolo.
7. Haga clic en **Close** cuando termine.

## Controlar el marco de tiempo del gráfico

El cuadro combinado **Timeframe** en la esquina superior derecha de la barra de pestañas establece qué tan atrás muestran el historial todos los gráficos de series temporales. Está oculto mientras la pestaña **Logs** está activa.

| Valor                    | Comportamiento | Notas |
|--------------------------|----------------|-------|
| 1 minute                 |                |       |
| 5 minutes *(predeterminado)* |                |       |
| 15 minutes               |                |       |
| 1 hour                   |                |       |
| 1 day                    |                |       |
| 1 week                   |                |       |

Seleccione un valor del menú desplegable **Timeframe**. Todos los gráficos visibles se actualizan inmediatamente.

## Usar la pestaña Logs

1. Seleccione la pestaña **Logs**.
2. La **Log path label** en la parte superior de la pestaña muestra la ruta completa del archivo de registro que se está siguiendo.
3. Use las casillas de verificación **Filter Categories (Logs)** para mostrar u ocultar categorías de registro individuales. La lista incluye una categoría **General** (mostrada por defecto) más cada categoría registrada con LogManager.
4. Haga clic en **Select All (Logs)** para habilitar todas las categorías a la vez.
5. Haga clic en **Deselect All (Logs)** para ocultar todas las categorías a la vez.
6. El botón de alternancia **Live / Paused** controla el desplazamiento automático:
   - **Live** — el visor se desplaza automáticamente a la salida más nueva a medida que llegan las líneas de registro.
   - **Paused** — el desplazamiento se detiene para que pueda leer líneas anteriores. Desplácese hacia arriba en cualquier momento para pausar automáticamente.
   - Haga clic en **Live** para reanudar y saltar al final del seguimiento.
7. Las líneas de registro se resaltan con sintaxis según el nivel de registro (DBG, INF, WRN, CRT, FTL) y el nombre de la categoría.

> **Nota:** El selector **Timeframe** está oculto mientras la pestaña **Logs** está activa. Cambie a cualquier otra pestaña para restaurarlo.

## Inspeccionar los diagnósticos de audio RX por flujo

1. Seleccione la pestaña **Audio**.
2. El gráfico principal muestra el llenado del búfer de reproducción (ms) y las subejecuciones/s a lo largo del tiempo.
3. Debajo del gráfico, un área de detalle muestra diagnósticos de audio RX por flujo para cada flujo de audio activo:
   - **Feed rate** — La tasa a la que se están alimentando los datos de audio al búfer de reproducción.
   - **Deficit** — El déficit actual del búfer en ms.
   - **Late packets** — Recuento de paquetes que llegan después de su tiempo de reproducción programado.
   - **Packet class code** — Clasificación de la calidad del paquete.
   - **Stream health** — Indicador general de salud del flujo de audio.
4. Use esta información para identificar qué flujo de audio está experimentando problemas y qué tipo de problema está ocurriendo.

## Qué significa cada indicador

| Indicador                              | Significado                                                                               |
|----------------------------------------|-------------------------------------------------------------------------------------------|
| **Status**                             | Calidad general del enlace, codificada por colores del verde (Excellent) al rojo (Poor). Estados: Excellent, Very Good, Good, Fair, Poor. |
| **Target Radio IP**                    | Dirección IP de la radio conectada. Muestra `Not connected` si no hay ninguna conexión activa. |
| **Selected Source**                    | NIC local o ruta de enlace utilizada para llegar a la radio.                              |
| **Local TCP**                          | Punto final TCP local (dirección y puerto).                                               |
| **Local UDP**                          | Punto final UDP local (dirección y puerto).                                               |
| **First UDP Packet**                   | Si se ha recibido el primer paquete UDP desde la conexión (Yes / No).                     |
| **Latency (RTT)**                      | Tiempo de ida y vuelta actual.                                                           |
| **Max Latency (RTT)**                  | RTT más alto visto desde la conexión.                                                     |
| **Audio / FFT / Waterfall / Meters / DAX rates** | Tasa de ingreso por categoría en kbps.                                          |
| **Total RX / Total TX**                | Bytes agregados por segundo en cada dirección.                                            |
| **Audio / FFT / Waterfall / Meters / DAX drops** | Recuentos y porcentaje de paquetes perdidos por categoría.                     |
| **RX Buffer Now / Peak**               | Llenado actual y máximo del búfer de audio en bytes y ms.                                |
| **Underruns (total / last sec)**       | Contadores de subejecuciones de audio.                                                    |
| **Audio Arrival Gap / Max Arrival Gap** | Temporización de llegada entre paquetes.                                                  |
| **Network Jitter**                     | Estimación de jitter suavizada del flujo de audio en ms.                                  |
| **Log path label**                     | Ruta completa del archivo de registro que se está siguiendo (visible en la pestaña Logs). |

## Referencia de controles

| Control                 | Tipo            | Predeterminado | Comportamiento                                                                                                                  |
|-------------------------|-----------------|----------------|---------------------------------------------------------------------------------------------------------------------------------|
| **Timeframe**           | Cuadro combinado | 5 minutes | Selecciona qué tan atrás muestran el historial los gráficos de series temporales. Oculto cuando la pestaña Logs está activa. |
| **Filter Categories (Logs)** | Casillas de verificación | — | Las casillas de verificación por categoría filtran la vista de registro. Incluye una categoría General más todas las categorías registradas de LogManager. |
| **Select All (Logs)**   | Botón           | —              | Muestra todas las categorías de registro en el visor.                                                                           |
| **Deselect All (Logs)** | Botón           | —              | Oculta todas las categorías de registro del visor.                                                                              |
| **Live / Paused (Logs)**| Botón de alternancia | Live         | Cuando está en Live, el visor se desplaza automáticamente a la salida más nueva. Desplazarse hacia arriba pausa automáticamente; hacer clic en Live reanuda y salta al final del seguimiento. |
| **Close**               | Botón           | —              | Cierra el diálogo.                                                                                                              |

## Consejos

- El diálogo actualiza todos los valores una vez por segundo. Si acaba de conectarse, espere un momento para que los campos se llenen.
- **Selected Source** es útil cuando el host tiene múltiples interfaces de red. Confirme que muestra la interfaz en la misma subred que la radio, no una VPN o un adaptador secundario.
- La pestaña **Rates** utiliza un eje Y logarítmico, lo que facilita la comparación de flujos de alto ancho de banda (como RX total a varios Mbps) junto con flujos de bajo ancho de banda (como Meters a unos pocos kbps) en el mismo gráfico.
- En la pestaña **Logs**, desplazarse hacia arriba cambia automáticamente la alternancia a **Paused**. Haga clic en **Live** para saltar al final del seguimiento actual.
- Los diagnósticos por flujo de la pestaña **Audio** le ayudan a identificar si los problemas de audio son causados por problemas de red (paquetes tardíos, alto déficit) o problemas de reproducción local (subejecuciones, mala gestión del búfer).

## Solución de problemas

- **Target Radio IP muestra `Not connected`** — No hay ninguna conexión activa con la radio. Use `Settings > Connect to Radio...` para descubrir y conectarse a su FLEX-8600, luego vuelva a abrir el diálogo.
- **Selected Source muestra una interfaz inesperada** — Su sistema operativo enrutó la conexión a través de una NIC diferente a la prevista. Verifique su tabla de enrutamiento o deshabilite las interfaces de red no utilizadas, luego vuelva a conectarse.
- **La tarjeta Status muestra Poor o Fair** — Verifique las pestañas **Latency** y **Packet Loss** para el rango de tiempo afectado. Un jitter alto o una pérdida de paquetes sostenida en el flujo de Audio generalmente indica congestión de red o interferencia Wi-Fi.
- **La pestaña Logs no muestra salida** — Es posible que todas las casillas de verificación de categoría estén deseleccionadas. Haga clic en **Select All (Logs)** para restaurar la visibilidad.
- **El flujo de audio muestra un recuento alto de paquetes tardíos** — Verifique la pestaña **Latency** para detectar picos de jitter y la pestaña **Packet Loss** para detectar pérdidas en el flujo de Audio. Considere aumentar el tamaño del búfer de audio en la configuración de audio.

## Relacionado

- [Network Diagnostics overview](overview.md)
- [Measure RTT and packet drops during audio problems](measure-rtt-and-packet-drops-during-audio-problems.md)
- [Check per-category data rates (audio, FFT, waterfall, meters, DAX)](check-per-category-data-rates-audio-fft-waterfall-meters-dax.md)
