# Ver la salida del registro en vivo filtrada por categoría de diagnóstico

La pestaña Logs en Diagnóstico de Red muestra un seguimiento en vivo del archivo de registro de AetherSDR, filtrado solo por las categorías de diagnóstico que usted elija. Úsela cuando necesite monitorear mensajes de un subsistema específico en tiempo real sin tener que revisar información no relacionada.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere una conexión de radio para ver el registro.
- Sepa qué categoría de diagnóstico desea monitorear (por ejemplo, `aether.connection`, `aether.cw`, `aether.dxcluster`).

## Pasos

1. Haga clic en `Settings > Network...` para abrir el diálogo de Diagnóstico de Red.
2. Haga clic en la pestaña **Logs**.
3. Revise la ruta del archivo de registro que se muestra en la **etiqueta de ruta del registro** en la parte superior de la pestaña para confirmar qué archivo se está siguiendo.
4. Marque o desmarque las casillas por categoría en **Filter Categories** para mostrar solo las categorías que desee. De forma predeterminada, la categoría **General** está disponible; todas las categorías de diagnóstico registradas aparecen junto a ella.
5. Para mostrar todas las categorías a la vez, haga clic en **Select All**. Para ocultar todas las categorías, haga clic en **Deselect All** y luego marque solo las categorías específicas que necesite.
6. Observe el visor. Las nuevas entradas se desplazan automáticamente mientras el conmutador muestre **Live**.
7. Cuando haya terminado, haga clic en **Close**.

## Función de cada control

| Control               | Comportamiento                                                                                                                                                                                                                                                    | Predeterminado |
|-----------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------|
| **Overview** (pestaña) | Muestra cuatro tarjetas de estado (Status, Latency, Packet Loss, Audio Buffer) y cuatro gráficos de series temporales (Latency and Jitter, Recent Packet Loss, Total Stream Rates, Audio Buffer).                                                                  | —              |
| **Details** (pestaña) | Cuadrícula desplazable con valores etiquetados para los grupos Network Status, Incoming Stream Rates, Packet Loss y Audio Playback.                                                                                                                               | —              |
| **Latency** (pestaña) | Gráfico de series temporales a ancho completo de RTT, intervalo de llegada y jitter en ms.                                                                                                                                                                        | —              |
| **Rates** (pestaña)   | Gráfico de series temporales a ancho completo en escala logarítmica de las tasas de bits entrantes por flujo (RX total, Audio, FFT, Waterfall, Meters, DAX) en kbps.                                                                                               | —              |
| **Packet Loss** (pestaña) | Gráfico de series temporales a ancho completo del porcentaje de pérdida de paquetes por categoría de flujo.                                                                                                                                                       | —              |
| **Audio** (pestaña)   | Gráfico de series temporales a ancho completo del llenado del búfer de reproducción (ms) y subejecuciones/s. Incluye diagnósticos de audio RX por flujo que muestran la tasa de alimentación, déficit, paquetes tardíos, código de clase de paquete y estado del flujo para cada flujo de audio activo. | —              |
| **Logs** (pestaña)    | Seguimiento en vivo del archivo de registro de AetherSDR filtrado por casillas de categoría. Resaltado de sintaxis por nivel de registro y nombre de categoría. El selector **Timeframe** está oculto mientras esta pestaña está activa.                         | —              |
| **Timeframe**         | Selecciona cuánto tiempo atrás muestran el historial los gráficos de series temporales. Oculto cuando la pestaña Logs está activa.                                                                                                                                 | 5 minutos      |
| **Filter Categories** | Casillas de verificación por categoría. Marque una categoría para incluir sus líneas; desmárquela para ocultarlas. Incluye **General** más todas las categorías registradas de LogManager.                                                                        | —              |
| **Select All**        | Muestra todas las categorías de registro en el visor de inmediato.                                                                                                                                                                                                | —              |
| **Deselect All**      | Oculta todas las categorías de registro del visor de inmediato.                                                                                                                                                                                                   | —              |
| **Live / Paused**     | Cuando está en **Live**, el visor se desplaza automáticamente a la salida más reciente. Desplazarse hacia arriba cambia el estado a **Paused**. Al hacer clic en el conmutador cuando muestra **Paused**, se reanuda el desplazamiento automático y salta al final. | Live           |
| **Log path label**    | Muestra la ruta completa del sistema de archivos del archivo de registro que se está siguiendo.                                                                                                                                                                   | —              |
| **Close**             | Cierra el diálogo.                                                                                                                                                                                                                                                | —              |

## Indicadores de Diagnóstico de Red

| Indicador | Descripción |
|---|---|
| **Status** | Calidad general del enlace: Excelente, Muy buena, Buena, Aceptable o Mala (codificado por color verde → rojo). |
| **Target Radio IP** | IP de la radio conectada, o 'No conectado'. |
| **Selected Source** | NIC local/ruta de enlace utilizada para la conexión. |
| **Local TCP** | Punto final TCP local. |
| **Local UDP** | Punto final UDP local. |
| **First UDP Packet** | Indica si se ha recibido el primer paquete UDP desde la conexión (Sí/No). |
| **Latency (RTT)** | Tiempo de ida y vuelta actual. |
| **Max Latency (RTT)** | RTT más alto observado desde la conexión. |
| **Audio / FFT / Waterfall / Meters / DAX rates** | Tasa de ingreso por categoría en kbps. |
| **Total RX / Total TX** | Bytes agregados por segundo en cada dirección. |
| **Audio / FFT / Waterfall / Meters / DAX drops** | Conteo y porcentaje de paquetes perdidos por categoría. |
| **RX Buffer Now / Peak** | Llenado actual y máximo del búfer de audio en bytes y ms. |
| **Underruns (total / last sec)** | Contadores de subejecución de audio. |
| **Audio Arrival Gap / Max Arrival Gap** | Temporización de llegada entre paquetes. |
| **Network Jitter** | Estimación de jitter suavizada del flujo de audio en ms. |

## Consejos

- El diálogo de Diagnóstico de Red respeta la configuración **FramelessWindow** de las preferencias de AetherSDR (`AppSettings > FramelessWindow`). Cuando está habilitado, el diálogo usa una geometría persistente que se guarda y restaura entre sesiones. Cuando está deshabilitado, el diálogo usa el marco de ventana estándar.
- La vista del registro se actualiza cada 500 ms, por lo que hay un breve retraso entre el momento en que se escribe un mensaje y su aparición en el visor.
- El resaltado de sintaxis por colores ayuda a distinguir los niveles de registro de un vistazo: las líneas `INF` aparecen en azul, `WRN` en ámbar y `CRT`/`FTL` en rojo. Los nombres de las categorías se muestran en negrita. Los números y los tokens de protocolo (como `UDP`, `TCP`, `RX`, `TX`) se resaltan por separado.
- Si desea congelar la pantalla para leer una entrada específica, desplácese hacia arriba. El visor cambia automáticamente a **Paused**. Haga clic en **Live** para volver al seguimiento.
- Hacer clic en **Deselect All** y luego marcar una sola categoría es la forma más rápida de aislar la salida de un subsistema.

## Relacionado

- [Pausar el desplazamiento del registro para inspeccionar una entrada anterior](pause-log-scrolling-to-inspect-an-older-entry.md)
- [Descripción general de Diagnóstico de Red](overview.md)
- [Medir RTT y pérdida de paquetes durante problemas de audio](measure-rtt-and-packet-drops-during-audio-problems.md)
