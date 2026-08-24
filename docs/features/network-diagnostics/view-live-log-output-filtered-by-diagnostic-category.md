# Ver la salida de registro en vivo filtrada por categoría de diagnóstico

La pestaña **Logs** en Network Diagnostics muestra una vista en vivo del archivo de registro de AetherSDR, filtrada únicamente por las categorías de diagnóstico que usted elija. Úsela cuando necesite observar mensajes específicos de subsistemas en tiempo real sin tener que revisar salidas no relacionadas.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere una conexión de radio para ver el registro.
- Sepa qué categoría de diagnóstico desea observar (por ejemplo, `aether.connection`, `aether.cw`, `aether.dxcluster`).

## Pasos

1. Haga clic en `Settings > Network...` para abrir el diálogo Network Diagnostics.
2. Haga clic en la pestaña **Logs**.
3. Revise la ruta del registro que se muestra en la **Log path label** en la parte superior de la pestaña para confirmar qué archivo se está siguiendo.
4. Marque o desmarque las casillas por categoría en **Filter Categories** para mostrar solo las categorías que desee. De forma predeterminada, la categoría **General** está disponible; todas las categorías de diagnóstico registradas aparecen junto a ella.
5. Para mostrar todas las categorías a la vez, haga clic en **Select All**. Para ocultar todas las categorías, haga clic en **Deselect All** y luego marque únicamente las categorías específicas que necesite.
6. Observe el visor. Las nuevas entradas se desplazan automáticamente mientras el conmutador indique **Live**.
7. Cuando haya terminado, haga clic en **Close**.

## Qué hace cada control

| Control                                | Comportamiento                                                                                                                                                                                                                                                                                         | Valor predeterminado                                                                                                                          |
|----------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------|
| **Overview** (pestaña)                     | Muestra cuatro tarjetas de estado (Status, Latency, Packet Loss, Audio Buffer) y cuatro gráficos de series temporales (Latency and Jitter, Recent Packet Loss, Total Stream Rates, Audio Buffer).                                                                                                                       | —                                                                                                                                             |
| **Connection Details** (página)          | Cuadrícula desplazable con valores etiquetados para Network Status, Incoming Stream Rates, Packet Loss, Audio Playback y la subsección Adaptive Frame-Rate Throttle. Incluye una acción Read-Only Clipboard Copy para copiar todo el resumen de diagnóstico. | Renombrado desde 'Details' en la reorganización de navegación por árbol de v26.8.4.                                                           |
| **Latency** (pestaña)                      | Gráfico de series temporales a ancho completo de RTT, diferencia de llegada y fluctuación (jitter) en ms.                                                                                                                                                                                              | —                                                                                                                                             |
| **Rates** (pestaña)                        | Gráfico de series temporales a ancho completo con escala logarítmica de las tasas de bits entrantes por flujo (RX total, Audio, FFT, Waterfall, Meters, DAX) en kbps.                                                                                                                                    | —                                                                                                                                             |
| **Packet Loss** (pestaña)                  | Gráfico de series temporales a ancho completo del porcentaje de pérdida de paquetes por categoría de flujo.                                                                                                                                                                                            | —                                                                                                                                             |
| **Audio** (pestaña)                        | Gráfico de series temporales a ancho completo del llenado del búfer de reproducción (ms) y subejecuciones (underruns) por segundo. Incluye diagnósticos de audio RX por flujo que muestran tasa de alimentación, déficit, paquetes tardíos, código de clase de paquete y salud del flujo para cada flujo de audio activo. | —                                                                                                                                             |
| **Logs** (pestaña)                         | Vista en vivo del archivo de registro de AetherSDR filtrada por casillas de categoría. Resaltado de sintaxis por nivel de registro y nombre de categoría. El selector **Timeframe** está oculto mientras esta pestaña está activa.                                                                         | —                                                                                                                                             |
| **TCI Clients** (página)                 | Enumera los clientes TCI conectados con un monitor de tráfico en vivo (Pause/Save log/Clear), controles de supresión de comandos de respuesta y detalles por cliente. Compilación condicionada por HAVE_TCI / soporte TCI. El selector Timeframe está oculto en esta página.                              | —                                                                                                                                             |
| **Timeframe**                          | Selecciona cuánto historial muestran los gráficos de series temporales. Oculto cuando la pestaña Logs está activa.                                                                                                                                                                                     | 5 minutos                                                                                                                                     |
| **Filter Categories**                  | Casillas por categoría. Marque una categoría para incluir sus líneas; desmárquela para ocultarlas. Incluye **General** y todas las categorías LogManager registradas.                                                                                                                                   | —                                                                                                                                             |
| **Select All**                         | Muestra inmediatamente todas las categorías de registro en el visor.                                                                                                                                                                                                                                   | —                                                                                                                                             |
| **Deselect All**                       | Oculta inmediatamente todas las categorías de registro del visor.                                                                                                                                                                                                                                      | —                                                                                                                                             |
| **Live / Paused**                      | Cuando está en **Live**, el visor se desplaza automáticamente a la salida más reciente. Desplazarse hacia arriba cambia el estado a **Paused**. Al hacer clic en el conmutador cuando indica **Paused**, se reanuda el desplazamiento automático y salta al final.                                   | Live                                                                                                                                           |
| **Log path label**                     | Muestra la ruta completa del sistema de archivos del archivo de registro que se está siguiendo.                                                                                                                                                                                                        | —                                                                                                                                             |
| **Close**                              | Cierra el diálogo.                                                                                                                                                                                                                                                                                     | —                                                                                                                                             |
| Adaptive Frame-Rate Throttle (sección) | Muestra los valores Current State, Pending Lift y Sessions This Run del regulador adaptativo. Reduce las tasas de fotogramas del panadapter cuando se detecta latencia o pérdida. Oculto hasta que haya datos del regulador disponibles.                                                                            | Nuevo en v26.8.4.                                                                                                                                 |
| Connection Details (página)              | Cuadrícula desplazable con valores etiquetados para Network Status, Incoming Stream Rates, Packet Loss, Audio Playback y la subsección Adaptive Frame-Rate Throttle. Incluye una acción Read-Only Clipboard Copy para copiar todo el resumen de diagnóstico. | Renombrado desde 'Details' en la reorganización de navegación por árbol de v26.8.4.                                                           |
| TCI Clients (página)                     | Enumera los clientes TCI conectados con un monitor de tráfico en vivo (Pause/Save log/Clear), controles de supresión de comandos de respuesta y detalles por cliente. Compilación condicionada por HAVE_TCI / soporte TCI. El selector Timeframe está oculto en esta página.                          | Nuevo en v26.8.4.                                                                                                                                 |

## Indicadores de Network Diagnostics

| Indicador | Descripción |
|---|---|
| **Status** | Calidad general del enlace: Excellent, Very Good, Good, Fair o Poor (codificado por colores de verde → rojo). |
| **Target Radio IP** | IP de la radio conectada, o 'Not connected'. |
| **Selected Source** | NIC local / ruta de enlace utilizada para la conexión. |
| **Local TCP** | Punto final TCP local. |
| **Local UDP** | Punto final UDP local. |
| **First UDP Packet** | Indica si el primer paquete UDP se ha recibido desde la conexión (Yes/No). |
| **Latency (RTT)** | Tiempo de ida y vuelta actual. Muestra "not measured on this link" cuando el transporte no tiene un viaje de ida y vuelta que medir. |
| **Max Latency (RTT)** | RTT más alto observado desde la conexión. Muestra "not measured on this link" cuando el transporte no tiene un viaje de ida y vuelta que medir. |
| **Audio / FFT / Waterfall / Meters / DAX rates** | Tasa de ingreso por categoría en kbps. Muestra "n/a" cuando el transporte no proporciona un desglose por categoría de flujo. |
| **Total RX / Total TX** | Bytes agregados por segundo en cada dirección. |
| **Audio / FFT / Waterfall / Meters / DAX drops** | Conteos y porcentajes de paquetes descartados por categoría. Muestra "n/a" cuando el transporte no proporciona un desglose por categoría de flujo. |
| **RX Buffer Now / Peak** | Llenado actual y máximo del búfer de audio en bytes y ms. |
| **Underruns (total / last sec)** | Contadores de subejecución (underrun) de audio. |
| **Audio Arrival Gap / Max Arrival Gap** | Temporización de llegada entre paquetes. Muestra "not measured on this link" cuando los datos de temporización de entrega no están disponibles. |
| **Network Jitter** | Estimación suavizada de fluctuación (jitter) del flujo de audio en ms. Muestra "not measured on this link" cuando los datos de temporización de entrega no están disponibles. |

## Consejos

- El diálogo Network Diagnostics respeta la configuración **FramelessWindow** de las preferencias de AetherSDR (`AppSettings > FramelessWindow`). Cuando está habilitada, el diálogo utiliza una geometría persistente que se guarda y restaura entre sesiones. Cuando está deshabilitada, el diálogo utiliza el marco de ventana estándar.
- La vista de registro se actualiza cada 500 ms, por lo que hay un breve retraso entre el momento en que se escribe un mensaje y su aparición en el visor.
- Los colores de resaltado de sintaxis ayudan a distinguir los niveles de registro de un vistazo: las líneas `INF` aparecen en azul, `WRN` en ámbar y `CRT`/`FTL` en rojo. Los nombres de categoría se muestran en negrita. Los números y tokens de protocolo (como `UDP`, `TCP`, `RX`, `TX`) se resaltan por separado.
- Si desea congelar la pantalla para leer una entrada específica, desplácese hacia arriba. El visor cambia a **Paused** automáticamente. Haga clic en **Live** para volver al final.
- Hacer clic en **Deselect All** y luego marcar una sola categoría es la forma más rápida de aislar la salida de un subsistema.
- En v26.7.4, el diálogo utiliza un árbol de navegación a la izquierda y un panel de contenido a la derecha. Haga clic en un nombre de página en el árbol **Network Diagnostics Navigation** para cambiar entre páginas. Un campo de búsqueda en la parte superior del árbol de navegación le permite filtrar las páginas disponibles por nombre.
- En v26.8.4, el diálogo se reorganizó a un árbol de categorías con páginas buscables: panel Overview, panel Connection Details (incluida la sección Adaptive Frame-Rate Throttle), Latency & Jitter, Stream Rates, Packet Loss, gráficos de tendencia de Audio, Application Logs, diagnósticos de audio RX por flujo y la página TCI Clients (condicionada por compilación).
- Cuando una métrica no puede medirse en el enlace actual (por ejemplo, RTT en un transporte sin viaje de ida y vuelta que medir), el diálogo muestra "not measured on this link" en lugar de un valor que podría confundirse con una lectura real. Los desgloses por flujo muestran "n/a" cuando el transporte lleva todo en un solo flujo.

## Relacionados

- [Pause log scrolling to inspect an older entry](pause-log-scrolling-to-inspect-an-older-entry.md)
- [Network Diagnostics overview](overview.md)
- [Measure RTT and packet drops during audio problems](measure-rtt-and-packet-drops-during-audio-problems.md)
