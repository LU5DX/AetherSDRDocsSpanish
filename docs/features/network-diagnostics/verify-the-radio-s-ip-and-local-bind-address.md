# Cuadro de diálogo de Diagnóstico de Red

Use esta página para supervisar el enlace de red en vivo entre AetherSDR y su FLEX-8600, confirmar las direcciones de conexión, inspeccionar las tasas de datos por flujo y revisar la salida de registro filtrada.

## Antes de comenzar

- AetherSDR debe estar en ejecución. El cuadro de diálogo no requiere una conexión activa a la radio, pero la mayoría de los campos y gráficos mostrarán valores significativos solo después de que se haya realizado un intento de conexión.

## Abrir el cuadro de diálogo

1. Haga clic en `Settings > Network...`.
2. Se abre el cuadro de diálogo **Network Diagnostics**. De forma predeterminada, se muestra la pestaña **Overview**.

## Resumen de las pestañas

El cuadro de diálogo está organizado en siete pestañas. Seleccione la pestaña que coincida con lo que desea inspeccionar.

| Pestaña            | Qué muestra                                                                                                                   |
|--------------------|-------------------------------------------------------------------------------------------------------------------------------|
| **Overview**       | Cuatro tarjetas de estado (Estado, Latencia, Pérdida de paquetes, Buffer de audio) y cuatro gráficos de series temporales (Latencia y fluctuación, Pérdida de paquetes reciente, Tasas totales de flujo, Buffer de audio). |
| **Details**        | Cuadrícula desplazable con valores etiquetados para los grupos de Estado de red, Tasas de flujo entrantes, Pérdida de paquetes y Reproducción de audio.     |
| **Latency**        | Gráfico de series temporales de ancho completo de RTT, intervalo de llegada y fluctuación en ms.                              |
| **Rates**          | Gráfico de series temporales de ancho completo con escala logarítmica de las tasas de bits entrantes por flujo (RX total, Audio, FFT, Waterfall, Meters, DAX) en kbps. |
| **Packet Loss**    | Gráfico de series temporales de ancho completo del % de pérdida de paquetes por categoría de flujo.                           |
| **Audio**          | Gráfico de series temporales de ancho completo del llenado del buffer de reproducción (ms) y subtramas/segundo.               |
| **Logs**           | Seguimiento en vivo del archivo de registro de AetherSDR, filtrado por casillas de verificación de categoría. Resaltado de sintaxis por nivel de registro y nombre de categoría. |

## Verificar la IP de la radio y la dirección de enlace local

1. Abra el cuadro de diálogo **Network Diagnostics** como se describió anteriormente.
2. Seleccione la pestaña **Details**.
3. Localice el grupo **Network Status**.
4. Lea **Target Radio IP** — esto muestra la dirección IP de la radio a la que se conectó AetherSDR. Si no se ha realizado ninguna conexión, el campo muestra `Not connected`.
5. Lea **Selected Source** — esto muestra la interfaz de red local o la ruta de enlace que AetherSDR utilizó para llegar a la radio.
6. Lea **Local TCP** y **Local UDP** para ver los puntos finales locales exactos de cada protocolo.
7. Haga clic en **Close** cuando haya terminado.

## Controlar el intervalo de tiempo del gráfico

El cuadro combinado **Timeframe** en la esquina superior derecha de la barra de pestañas establece cuánto tiempo hacia atrás muestran el historial todos los gráficos de series temporales. Está oculto mientras la pestaña **Logs** está activa.

| Valor        |
|--------------|
| 1 minute     |
| 5 minutes *(predeterminado)* |
| 15 minutes   |
| 1 hour       |
| 1 day        |
| 1 week       |

Seleccione un valor del menú desplegable **Timeframe**. Todos los gráficos visibles se actualizan inmediatamente.

## Usar la pestaña Logs

1. Seleccione la pestaña **Logs**.
2. La **etiqueta de ruta de registro** en la parte superior de la pestaña muestra la ruta completa del archivo de registro que se está siguiendo.
3. Use las casillas de verificación **Filter Categories (Logs)** para mostrar u ocultar categorías de registro individuales. La lista incluye una categoría **General** (mostrada de forma predeterminada) más todas las categorías registradas con LogManager.
4. Haga clic en **Select All (Logs)** para habilitar todas las categorías a la vez.
5. Haga clic en **Deselect All (Logs)** para ocultar todas las categorías a la vez.
6. El botón de alternancia **Live / Paused** controla el desplazamiento automático:
   - **Live** — el visor se desplaza automáticamente a la salida más reciente a medida que llegan las líneas de registro.
   - **Paused** — el desplazamiento se detiene para que pueda leer líneas anteriores. Desplácese hacia arriba en cualquier momento para pausar automáticamente.
   - Haga clic en **Live** para reanudar y saltar al final del seguimiento.
7. Las líneas de registro se resaltan sintácticamente por nivel de registro (DBG, INF, WRN, CRT, FTL) y por nombre de categoría.

> **Nota:** El selector **Timeframe** está oculto mientras la pestaña **Logs** está activa. Cambie a cualquier otra pestaña para restaurarlo.

## Qué significa cada indicador

| Indicador                               | Significado                                                                                 |
|-----------------------------------------|---------------------------------------------------------------------------------------------|
| **Status**                              | Calidad general del enlace, codificada por colores de verde (Excelente) a rojo (Deficiente). Estados: Excelente, Muy bueno, Bueno, Aceptable, Deficiente. |
| **Target Radio IP**                     | Dirección IP de la radio conectada. Muestra `Not connected` si no hay ninguna conexión activa. |
| **Selected Source**                     | NIC local o ruta de enlace utilizada para llegar a la radio.                                |
| **Local TCP**                           | Punto final TCP local (dirección y puerto).                                                  |
| **Local UDP**                           | Punto final UDP local (dirección y puerto).                                                  |
| **First UDP Packet**                    | Indica si se ha recibido el primer paquete UDP desde la conexión (Sí / No).                  |
| **Latency (RTT)**                       | Tiempo de ida y vuelta actual.                                                               |
| **Max Latency (RTT)**                   | RTT más alto observado desde la conexión.                                                     |
| **Audio / FFT / Waterfall / Meters / DAX rates** | Tasa de ingreso por categoría en kbps.                                            |
| **Total RX / Total TX**                 | Bytes agregados por segundo en cada dirección.                                               |
| **Audio / FFT / Waterfall / Meters / DAX drops** | Recuentos de paquetes perdidos por categoría y porcentaje.                         |
| **RX Buffer Now / Peak**                | Llenado actual y máximo del buffer de audio en bytes y ms.                                   |
| **Underruns (total / last sec)**        | Contadores de subtramas de audio.                                                             |
| **Audio Arrival Gap / Max Arrival Gap** | Temporización de llegada entre paquetes.                                                      |
| **Network Jitter**                      | Estimación de fluctuación suavizada del flujo de audio en ms.                                 |
| **Log path label**                      | Ruta completa del archivo de registro que se está siguiendo (visible en la pestaña Logs).     |

## Referencia de controles

| Control                  | Tipo           | Predeterminado | Comportamiento                                                                                                                   |
|--------------------------|----------------|----------------|----------------------------------------------------------------------------------------------------------------------------------|
| **Timeframe**            | Cuadro combinado | 5 minutes     | Selecciona cuánto tiempo hacia atrás muestran el historial los gráficos de series temporales. Oculto cuando la pestaña Logs está activa. |
| **Filter Categories (Logs)** | Casillas de verificación | —      | Casillas de verificación por categoría que filtran la vista de registro. Incluye una categoría General más todas las categorías de LogManager registradas. |
| **Select All (Logs)**    | Botón          | —              | Muestra todas las categorías de registro en el visor.                                                                            |
| **Deselect All (Logs)**  | Botón          | —              | Oculta todas las categorías de registro del visor.                                                                               |
| **Live / Paused (Logs)** | Botón de alternancia | Live         | Cuando está en Live, el visor se desplaza automáticamente a la salida más reciente. Desplazarse hacia arriba pausa automáticamente; al hacer clic en Live se reanuda y salta al final del seguimiento. |
| **Close**                | Botón          | —              | Cierra el cuadro de diálogo.                                                                                                     |

## Consejos

- El cuadro de diálogo actualiza todos los valores una vez por segundo. Si acaba de conectarse, espere un momento para que los campos se llenen.
- **Selected Source** es útil cuando el host tiene múltiples interfaces de red. Confirme que muestra la interfaz en la misma subred que la radio, no una VPN o un adaptador secundario.
- La pestaña **Rates** utiliza un eje y logarítmico, lo que facilita la comparación de flujos de alto ancho de banda (como RX total a varios Mbps) junto con flujos de bajo ancho de banda (como Meters a unos pocos kbps) en el mismo gráfico.
- En la pestaña **Logs**, desplazarse hacia arriba cambia automáticamente la alternancia a **Paused**. Haga clic en **Live** para saltar al final del seguimiento actual.

## Solución de problemas

- **Target Radio IP muestra `Not connected`** — No hay ninguna conexión activa a la radio. Use `Settings > Connect to Radio...` para descubrir y conectarse a su FLEX-8600, luego vuelva a abrir el cuadro de diálogo.
- **Selected Source muestra una interfaz inesperada** — Su sistema operativo enrutó la conexión a través de una NIC diferente a la prevista. Verifique su tabla de enrutamiento o deshabilite las interfaces de red no utilizadas, luego vuelva a conectarse.
- **La tarjeta de estado muestra Poor o Fair** — Revise las pestañas **Latency** y **Packet Loss** para el rango de tiempo afectado. Una fluctuación alta o una pérdida sostenida de paquetes en el flujo de audio generalmente indican congestión de red o interferencia de Wi-Fi.
- **La pestaña Logs no muestra salida** — Es posible que todas las casillas de verificación de categoría estén deseleccionadas. Haga clic en **Select All (Logs)** para restaurar la visibilidad.

## Relacionado

- [Network Diagnostics overview](overview.md)
- [Measure RTT and packet drops during audio problems](measure-rtt-and-packet-drops-during-audio-problems.md)
- [Check per-category data rates (audio, FFT, waterfall, meters, DAX)](check-per-category-data-rates-audio-fft-waterfall-meters-dax.md)
