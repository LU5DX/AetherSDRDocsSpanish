# Ver la salida de registro en vivo filtrada por categoría de diagnóstico

La pestaña Logs en Network Diagnostics muestra un seguimiento en vivo del archivo de registro de AetherSDR, filtrado solo por las categorías de diagnóstico que usted elija. Úselo cuando necesite observar mensajes específicos de un subsistema en tiempo real sin tener que revisar información no relacionada.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere una conexión de radio para ver el registro.
- Sepa qué categoría de diagnóstico desea observar (por ejemplo, `aether.connection`, `aether.cw`, `aether.dxcluster`).

## Pasos

1. Haga clic en `Settings > Network...` para abrir el cuadro de diálogo Network Diagnostics.
2. Haga clic en la pestaña **Logs**.
3. Revise la ruta del archivo de registro que se muestra en la **etiqueta de ruta de registro** en la parte superior de la pestaña para confirmar qué archivo se está supervisando.
4. Marque o desmarque las casillas por categoría en **Filter Categories** para mostrar solo las categorías que desee. De forma predeterminada, la categoría **General** está disponible; todas las categorías de diagnóstico registradas aparecen junto a ella.
5. Para mostrar todas las categorías a la vez, haga clic en **Select All**. Para ocultar todas las categorías, haga clic en **Deselect All** y luego marque solo las categorías específicas que necesite.
6. Observe el visor. Las nuevas entradas se desplazan automáticamente mientras el conmutador muestre **Live**.
7. Cuando termine, haga clic en **Close**.

## Qué hace cada control

| Control | Comportamiento | Por defecto |
|---|---|---|
| **Overview** (pestaña) | Muestra cuatro tarjetas de estado (Status, Latency, Packet Loss, Audio Buffer) y cuatro gráficos de series temporales (Latencia y Jitter, Pérdida reciente de paquetes, Tasas totales de flujo, Buffer de audio). | — |
| **Details** (pestaña) | Cuadrícula desplazable con valores etiquetados para los grupos Network Status, Incoming Stream Rates, Packet Loss y Audio Playback. | — |
| **Latency** (pestaña) | Gráfico de series temporales a ancho completo de RTT, intervalo de llegada y jitter en ms. | — |
| **Rates** (pestaña) | Gráfico de series temporales a ancho completo con escala logarítmica de las tasas de bits entrantes por flujo (RX total, Audio, FFT, Waterfall, Meters, DAX) en kbps. | — |
| **Packet Loss** (pestaña) | Gráfico de series temporales a ancho completo del porcentaje de pérdida de paquetes por categoría de flujo. | — |
| **Audio** (pestaña) | Gráfico de series temporales a ancho completo del llenado del buffer de reproducción (ms) y de las interrupciones por segundo. | — |
| **Logs** (pestaña) | Seguimiento en vivo del archivo de registro de AetherSDR filtrado por casillas de verificación de categoría. Resaltado de sintaxis por nivel de registro y nombre de categoría. El selector **Timeframe** está oculto mientras esta pestaña esté activa. | — |
| **Timeframe** | Selecciona cuánto tiempo hacia atrás muestran los gráficos de series temporales. Oculto cuando la pestaña Logs está activa. | 5 minutos |
| **Filter Categories** | Casillas de verificación por categoría. Marque una categoría para incluir sus líneas; desmárquela para ocultarlas. Incluye **General** más todas las categorías de LogManager registradas. | — |
| **Select All** | Muestra inmediatamente todas las categorías de registro en el visor. | — |
| **Deselect All** | Oculta inmediatamente todas las categorías de registro del visor. | — |
| **Live / Paused** | Cuando está en **Live**, el visor se desplaza automáticamente a la salida más reciente. Desplazarse hacia arriba cambia el estado a **Paused**. Al hacer clic en el conmutador cuando muestra **Paused** se reanuda el desplazamiento automático y se salta al final. | Live |
| **Log path label** | Muestra la ruta completa del sistema de archivos del archivo de registro que se está supervisando. | — |
| **Close** | Cierra el cuadro de diálogo. | — |

## Indicadores de Network Diagnostics

| Indicador | Descripción |
|---|---|
| **Status** | Calidad general del enlace: Excelente, Muy buena, Buena, Aceptable o Pobre (codificado por colores de verde a rojo). |
| **Target Radio IP** | IP de la radio conectada, o 'Not connected'. |
| **Selected Source** | NIC local/ruta de enlace utilizada para la conexión. |
| **Local TCP** | Punto final TCP local. |
| **Local UDP** | Punto final UDP local. |
| **First UDP Packet** | Indica si se ha recibido el primer paquete UDP desde la conexión (Sí/No). |
| **Latency (RTT)** | Tiempo de ida y vuelta actual. |
| **Max Latency (RTT)** | RTT más alto observado desde la conexión. |
| **Audio / FFT / Waterfall / Meters / DAX rates** | Tasa de ingreso por categoría en kbps. |
| **Total RX / Total TX** | Bytes agregados por segundo en cada dirección. |
| **Audio / FFT / Waterfall / Meters / DAX drops** | Conteo y porcentaje de paquetes perdidos por categoría. |
| **RX Buffer Now / Peak** | Llenado actual y máximo del buffer de audio en bytes y ms. |
| **Underruns (total / last sec)** | Contadores de interrupciones de audio. |
| **Audio Arrival Gap / Max Arrival Gap** | Temporización de llegada entre paquetes. |
| **Network Jitter** | Estimación suavizada de jitter del flujo de audio en ms. |

## Consejos

- El cuadro de diálogo Network Diagnostics respeta la configuración **FramelessWindow** de las preferencias de AetherSDR (`AppSettings > FramelessWindow`). Cuando está habilitado, el diálogo usa una geometría persistente que se guarda y restaura entre sesiones. Cuando está deshabilitado, el diálogo usa el marco de ventana estándar.
- La vista de registro se actualiza cada 500 ms, por lo que hay un breve retraso entre que se escribe un mensaje y que aparece en el visor.
- Los colores de resaltado de sintaxis ayudan a distinguir los niveles de registro de un vistazo: las líneas `INF` aparecen en azul, `WRN` en ámbar y `CRT`/`FTL` en rojo. Los nombres de las categorías se muestran en negrita. Los números y los tokens de protocolo (como `UDP`, `TCP`, `RX`, `TX`) se resaltan por separado.
- Si desea congelar la pantalla para leer una entrada específica, desplácese hacia arriba. El visor cambia a **Paused** automáticamente. Haga clic en **Live** para volver al final.
- Haga clic en **Deselect All** y luego marque una sola categoría; esta es la forma más rápida de aislar la salida de un subsistema.

## Relacionados

- [Pause log scrolling to inspect an older entry](pause-log-scrolling-to-inspect-an-older-entry.md)
- [Network Diagnostics overview](overview.md)
- [Measure RTT and packet drops during audio problems](measure-rtt-and-packet-drops-during-audio-problems.md)
