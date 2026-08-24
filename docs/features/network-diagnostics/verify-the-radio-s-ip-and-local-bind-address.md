# Cuadro de diálogo de Diagnóstico de Red

Utilice esta página para monitorear el enlace de red en vivo entre AetherSDR y su FLEX-8600, confirmar las direcciones de conexión, inspeccionar las tasas de datos por flujo y revisar la salida de registros filtrada.

## Antes de comenzar

- AetherSDR debe estar en ejecución. El cuadro de diálogo no requiere una conexión de radio activa, pero la mayoría de los campos y gráficos mostrarán valores significativos solo después de que se haya realizado un intento de conexión.

## Abrir el cuadro de diálogo

1. Haga clic en `Settings > Network...`.
2. Se abre el cuadro de diálogo **Network Diagnostics**. De forma predeterminada, muestra un árbol de navegación a la izquierda con un panel de contenido a la derecha. La vista predeterminada es **Overview**.

## Descripción general del diseño

El cuadro de diálogo utiliza un diseño de dos paneles con un árbol de navegación a la izquierda y un panel de contenido a la derecha. Haga clic en cualquier elemento del árbol de navegación para mostrar la página correspondiente.

El árbol de navegación contiene las siguientes secciones y páginas:

- **Radio Connection**
  - Overview
  - Connection Details
- **Network Graphs**
  - Latency
  - Rates
  - Packet Loss
  - Audio
- **Logging**
  - Logs
- **TCI Clients** *(limitado por compilación, se muestra solo cuando el soporte TCI está compilado)*

## Buscar una página

1. Localice el campo de búsqueda en la parte superior del árbol de navegación, identificado con un icono de lupa.
2. Escriba cualquier parte del nombre de una página (por ejemplo, "delay" o "rates"). El árbol de navegación se filtra para mostrar solo los elementos coincidentes.
3. Haga clic en un elemento filtrado para abrir esa página.
4. Borre el campo de búsqueda para restaurar el árbol de navegación completo.

## Resumen de páginas

| Página                    | Qué muestra                                                                                                                                                                                                 |
|---------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Overview**              | Cuatro tarjetas de estado (Status, Latency, Packet Loss, Audio Buffer) y cuatro gráficos de series temporales (Latency and Jitter, Recent Packet Loss, Total Stream Rates, Audio Buffer).                    |
| **Connection Details**    | Cuadrícula desplazable con valores etiquetados para los grupos Network Status, Incoming Stream Rates, Packet Loss y Audio Playback, además de la subsección Adaptive Frame-Rate Throttle. Renombrada desde "Details" en la reorganización del árbol de navegación de v26.8.4. Incluye una acción de copia al portapapeles de solo lectura para copiar el resumen de diagnóstico completo. |
| **Latency**               | Gráfico de series temporales de ancho completo de RTT, intervalo de llegada y jitter en ms.                                                                                                                 |
| **Rates**                 | Gráfico de series temporales de ancho completo con escala logarítmica de las tasas de bits entrantes por flujo (RX total, Audio, FFT, Waterfall, Meters, DAX) en kbps.                                      |
| **Packet Loss**           | Gráfico de series temporales de ancho completo del porcentaje de pérdida de paquetes por categoría de flujo.                                                                                                |
| **Audio**                 | Gráfico de series temporales de ancho completo del llenado del búfer de reproducción (ms) y underruns/s. Incluye diagnósticos de audio RX por flujo que muestran la tasa de alimentación, el déficit, los paquetes tardíos, el código de clase de paquete y el estado del flujo para cada flujo de audio activo. |
| **Logs**                  | Cola en vivo del archivo de registro de AetherSDR, filtrada por casillas de verificación de categoría. Resaltado de sintaxis por nivel de registro y nombre de categoría. El selector de período de tiempo está oculto mientras esta página está activa. |
| **TCI Clients**           | Enumera los clientes TCI conectados con un monitor de tráfico en vivo (Pause/Save log/Clear), controles de supresión de comandos de respuesta y detalles por cliente. Nuevo en v26.8.4. Limitado por compilación mediante HAVE_TCI / soporte TCI. El selector de período de tiempo está oculto en esta página. |

## Verificar la IP de la radio y la dirección de enlace local

1. Abra el cuadro de diálogo **Network Diagnostics** como se describió anteriormente.
2. En el árbol de navegación, haga clic en **Connection Details**.
3. Localice el grupo **Network Status**.
4. Lea **Target Radio IP** — esto muestra la dirección IP de la radio a la que AetherSDR está conectado. Si no se ha realizado ninguna conexión, el campo muestra `Not connected`.
5. Lea **Selected Source** — esto muestra la interfaz de red local o la ruta de enlace que AetherSDR utilizó para llegar a la radio.
6. Lea **Local TCP** y **Local UDP** para ver los puntos finales locales exactos de cada protocolo.
7. Haga clic en **Close** cuando haya terminado.

## Revisar el Adaptive Frame-Rate Throttle

La página **Connection Details** incluye una sección **Adaptive Frame-Rate Throttle** que muestra:

- **Current State** — Si el throttling está activo actualmente.
- **Pending Lift** — Si hay una liberación del throttling pendiente.
- **Sessions This Run** — Número de sesiones de throttling desde la conexión.

Este throttle reduce las tasas de fotogramas del panadapter cuando se detecta latencia o pérdida de paquetes en el enlace. La sección está oculta hasta que los datos de throttling estén disponibles.

## Controlar el período de tiempo de los gráficos

El cuadro combinado **Timeframe** en la esquina superior derecha establece cuánto historial muestran todos los gráficos de series temporales. Está oculto mientras la página **Logs** o **TCI Clients** está activa.

| Valor                                  | Comportamiento                                                                                                                                                     | Notas                                                                                                                                          |
|----------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------|
| 1 minute                               |                                                                                                                                                                      |                                                                                                                                                |
| 5 minutes *(predeterminado)*           |                                                                                                                                                                      |                                                                                                                                                |
| 15 minutes                             |                                                                                                                                                                      |                                                                                                                                                |
| 1 hour                                 |                                                                                                                                                                      |                                                                                                                                                |
| 1 day                                  |                                                                                                                                                                      |                                                                                                                                                |
| 1 week                                 |                                                                                                                                                                      |                                                                                                                                                |

Seleccione un valor en el menú desplegable **Timeframe**. Todos los gráficos visibles se actualizan inmediatamente.

## Usar la página Logs

1. En el árbol de navegación, haga clic en **Logs**.
2. La **Log path label** en la parte superior de la página muestra la ruta completa del archivo de registro que se está siguiendo.
3. Use las casillas de verificación **Filter Categories (Logs)** para mostrar u ocultar categorías de registro individuales. La lista incluye una categoría **General** (mostrada de forma predeterminada) más todas las categorías registradas con LogManager.
4. Haga clic en **Select All (Logs)** para habilitar todas las categorías a la vez.
5. Haga clic en **Deselect All (Logs)** para ocultar todas las categorías a la vez.
6. El botón de alternancia **Live / Paused** controla el desplazamiento automático:
   - **Live** — el visor se desplaza automáticamente a la salida más reciente a medida que llegan líneas de registro.
   - **Paused** — el desplazamiento está detenido para que pueda leer líneas anteriores. Desplácese hacia arriba en cualquier momento para pausar automáticamente.
   - Haga clic en **Live** para reanudar y saltar de nuevo a la cola.
7. Las líneas de registro tienen resaltado de sintaxis por nivel de registro (DBG, INF, WRN, CRT, FTL) y por nombre de categoría.

> **Nota:** El selector **Timeframe** está oculto mientras la página **Logs** está activa. Navegue a cualquier otra página para restaurarlo.

## Usar la página TCI Clients *(limitado por compilación)*

> **Nota:** Esta página aparece solo en compilaciones con soporte TCI compilado (`HAVE_TCI`).

1. En el árbol de navegación, haga clic en **TCI Clients**.
2. La página enumera todos los clientes TCI conectados.
3. Para cada cliente, revise los detalles por cliente, como el estado de la conexión y la actividad de tráfico.
4. Use los controles del monitor de tráfico:
   - **Pause** — congele la visualización de tráfico en vivo.
   - **Save log** — exporte el registro de tráfico capturado a un archivo.
   - **Clear** — restablezca el monitor de tráfico.
5. Use los controles de supresión de comandos de respuesta para evitar que AetherSDR responda a comandos TCI específicos, si es necesario.

> **Nota:** El selector **Timeframe** está oculto mientras esta página está activa.

## Inspeccionar los diagnósticos de audio RX por flujo

1. En el árbol de navegación, haga clic en **Audio**.
2. El gráfico principal muestra el llenado del búfer de reproducción (ms) y los underruns/s a lo largo del tiempo.
3. Debajo del gráfico, un área de detalle muestra los diagnósticos de audio RX por flujo para cada flujo de audio activo:
   - **Feed rate** — La tasa a la que se alimentan los datos de audio al búfer de reproducción.
   - **Deficit** — El déficit actual del búfer en ms.
   - **Late packets** — Número de paquetes que llegan después de su tiempo de reproducción programado.
   - **Packet class code** — Clasificación de la calidad del paquete.
   - **Stream health** — Indicador general de salud del flujo de audio.
4. Use esta información para identificar qué flujo de audio está experimentando problemas y qué tipo de problema está ocurriendo.

## Qué significa cada indicador

| Indicador                               | Significado                                                                             |
|-----------------------------------------|-----------------------------------------------------------------------------------------|
| **Status**                              | Calidad general del enlace, codificada por colores desde verde (Excellent) hasta rojo (Poor). Estados: Excellent, Very Good, Good, Fair, Poor. |
| **Target Radio IP**                     | Dirección IP de la radio conectada. Muestra `Not connected` si no hay ninguna conexión activa. |
| **Selected Source**                     | NIC local o ruta de enlace utilizada para llegar a la radio.                            |
| **Local TCP**                           | Punto final TCP local (dirección y puerto).                                             |
| **Local UDP**                           | Punto final UDP local (dirección y puerto).                                             |
| **First UDP Packet**                    | Si el primer paquete UDP se ha recibido desde la conexión (Yes / No).                   |
| **Latency (RTT)**                       | Tiempo de ida y vuelta actual. Muestra "not measured on this link" si el transporte no tiene ida y vuelta que medir. |
| **Max Latency (RTT)**                   | RTT más alto visto desde la conexión. Muestra "not measured on this link" si el transporte no tiene ida y vuelta que medir. |
| **Audio / FFT / Waterfall / Meters / DAX rates** | Tasa de ingreso por categoría en kbps. Muestra "n/a" en transportes que no exponen estadísticas de categoría por flujo. |
| **Total RX / Total TX**                 | Bytes agregados por segundo en cada dirección.                                          |
| **Audio / FFT / Waterfall / Meters / DAX drops** | Conteos de paquetes perdidos y porcentaje por categoría. Muestra "n/a" en transportes que no exponen estadísticas de categoría por flujo. |
| **RX Buffer Now / Peak**                | Llenado actual y máximo del búfer de audio en bytes y ms.                               |
| **Underruns (total / last sec)**        | Contadores de underrun de audio.                                                        |
| **Audio Arrival Gap / Max Arrival Gap** | Temporización de llegada entre paquetes. Muestra "not measured on this link" antes de que se cierre la primera ventana de temporización o si el transporte no informa temporización. |
| **Network Jitter**                      | Estimación de jitter suavizada del flujo de audio en ms. Muestra "not measured on this link" antes de que se cierre la primera ventana de temporización o si el transporte no informa temporización. |
| **Log path label**                      | Ruta completa del archivo de registro que se está siguiendo (visible en la página Logs).|

## Referencia de controles

| Control                      | Tipo           | Predeterminado | Comportamiento                                                                                                                          |
|------------------------------|----------------|----------------|-----------------------------------------------------------------------------------------------------------------------------------------|
| **Timeframe**                | Cuadro combinado | 5 minutes   | Selecciona cuánto historial muestran los gráficos de series temporales. Oculto cuando la página Logs o TCI Clients está activa.        |
| **Filter Categories (Logs)** | Casillas de verificación | —          | Las casillas de verificación por categoría filtran la vista de registro. Incluye una categoría General más todas las categorías registradas de LogManager. |
| **Select All (Logs)**        | Botón          | —              | Muestra todas las categorías de registro en el visor.                                                                                   |
| **Deselect All (Logs)**      | Botón          | —              | Oculta todas las categorías de registro del visor.                                                                                      |
| **Live / Paused (Logs)**     | Botón de alternancia | Live        | Cuando está en Live, el visor se desplaza automáticamente a la salida más reciente. Desplazarse hacia arriba pausa automáticamente; hacer clic en Live reanuda y salta a la cola. |
| **Close**                    | Botón          | —              | Cierra el cuadro de diálogo.                                                                                                            |

## Consejos

- El cuadro de diálogo actualiza todos los valores una vez por segundo. Si acaba de conectarse, espere un momento para que los campos se llenen.
- **Selected Source** es útil cuando el host tiene múltiples interfaces de red. Confirme que muestra la interfaz en la misma subred que la radio, no una VPN o un adaptador secundario.
- La página **Rates** utiliza un eje y logarítmico, lo que facilita comparar flujos de alto ancho de banda (como RX total a varios Mbps) junto con flujos de bajo ancho de banda (como Meters a unos pocos kbps) en el mismo gráfico.
- En la página **Logs**, desplazarse hacia arriba cambia automáticamente la alternancia a **Paused**. Haga clic en **Live** para saltar de nuevo a la cola actual.
- Los diagnósticos por flujo de la página **Audio** le ayudan a identificar si los problemas de audio son causados por problemas de red (paquetes tardíos, déficit alto) o problemas de reproducción local (underruns, mala gestión del búfer).
- Use el campo de búsqueda en la parte superior del árbol de navegación para encontrar rápidamente cualquier página por nombre.
- En transportes sin ida y vuelta que medir, los indicadores **Latency (RTT)** y **Max Latency (RTT)** muestran "not measured on this link" en lugar de un valor engañoso "< 1 ms". Cuando las estadísticas de categoría por flujo no están disponibles, los campos de tasa y pérdida muestran "n/a" en lugar de filas en cero.

## Solución de problemas

- **Target Radio IP muestra `Not connected`** — No hay ninguna conexión activa con la radio. Use `Settings > Connect to Radio...` para descubrir y conectarse a su FLEX-8600, luego vuelva a abrir el cuadro de diálogo.
- **Selected Source muestra una interfaz inesperada** — Su sistema operativo enrutó la conexión a través de una NIC diferente a la prevista. Verifique su tabla de enrutamiento o deshabilite las interfaces de red no utilizadas, luego vuelva a conectarse.
- **La tarjeta Status muestra Poor o Fair** — Revise las páginas **Latency** y **Packet Loss** para el rango de tiempo afectado. Un jitter alto o una pérdida de paquetes sostenida en el flujo de Audio generalmente indica congestión de red o interferencia de Wi-Fi.
- **La página Logs no muestra salida** — Es posible que todas las casillas de verificación de categoría estén deseleccionadas. Haga clic en **Select All (Logs)** para restaurar la visibilidad.
- **El flujo de Audio muestra un alto conteo de paquetes tardíos** — Revise la
