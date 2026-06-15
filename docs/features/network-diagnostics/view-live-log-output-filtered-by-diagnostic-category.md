# Ver la salida de registro en vivo filtrada por categoría de diagnóstico

La pestaña Registros en Diagnóstico de Red muestra un seguimiento en vivo del archivo de registro de AetherSDR, filtrado solo por las categorías de diagnóstico que usted elija. Úselo cuando necesite monitorear mensajes de subsistemas específicos en tiempo real sin tener que revisar salida no relacionada.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere una conexión de radio para ver el registro.
- Sepa qué categoría de diagnóstico desea monitorear (por ejemplo, `aether.connection`, `aether.cw`, `aether.dxcluster`).

## Pasos

1. Haga clic en `Settings > Network...` para abrir el diálogo Diagnóstico de Red.
2. Haga clic en la pestaña **Logs**.
3. Revise la ruta del registro que se muestra en la **etiqueta de ruta de registro** en la parte superior de la pestaña para confirmar qué archivo se está siguiendo.
4. Marque o desmarque las casillas por categoría debajo de **Filter Categories** para mostrar solo las categorías que desee. De forma predeterminada, la categoría **General** está disponible; todas las categorías de diagnóstico registradas aparecen junto a ella.
5. Para mostrar todas las categorías a la vez, haga clic en **Select All**. Para ocultar todas las categorías, haga clic en **Deselect All**, luego marque solo las categorías específicas que necesite.
6. Observe el visor. Las nuevas entradas se desplazan automáticamente mientras el botón de alternancia muestre **Live**.
7. Cuando haya terminado, haga clic en **Close**.

## Qué hace cada control

| Control               | Comportamiento                                                                                                                                                                                                                         | Predeterminado |
|-----------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------|
| **Overview** (pestaña)    | Muestra cuatro tarjetas de estado (Estado, Latencia, Pérdida de Paquetes, Buffer de Audio) y cuatro gráficos de series temporales (Latencia y Jitter, Pérdida de Paquetes Reciente, Tasas de Transmisión Totales, Buffer de Audio).      | —              |
| **Details** (pestaña)     | Cuadrícula desplazable con valores etiquetados para los grupos Estado de Red, Tasas de Transmisión Entrante, Pérdida de Paquetes y Reproducción de Audio.                                                                            | —              |
| **Latency** (pestaña)     | Gráfico de series temporales de ancho completo de RTT, intervalo de llegada y jitter en ms.                                                                                                                                               | —              |
| **Rates** (pestaña)       | Gráfico de series temporales de ancho completo con escala logarítmica de las tasas de bits entrantes por flujo (Total RX, Audio, FFT, Waterfall, Medidores, DAX) en kbps.                                                         | —              |
| **Packet Loss** (pestaña) | Gráfico de series temporales de ancho completo del % de pérdida de paquetes por categoría de flujo.                                                                                                                                       | —              |
| **Audio** (pestaña)       | Gráfico de series temporales de ancho completo del llenado del buffer de reproducción (ms) y subtasa de subejecuciones. Incluye diagnósticos de audio RX por flujo que muestran la tasa de alimentación, déficit, paquetes tardíos, código de clase de paquete y estado del flujo para cada flujo de audio activo. | —              |
| **Logs** (pestaña)        | Seguimiento en vivo del archivo de registro de AetherSDR filtrado por casillas de categoría. Resaltado de sintaxis por nivel de registro y nombre de categoría. El selector **Timeframe** está oculto mientras esta pestaña está activa. | —              |
| **Timeframe**         | Selecciona cuánto tiempo atrás muestran los gráficos de series temporales el historial. Oculto cuando la pestaña Registros está activa.                                                                                             | 5 minutos      |
| **Filter Categories** | Casillas de verificación por categoría. Marque una categoría para incluir sus líneas; desmárquela para ocultarlas. Incluye **General** más todas las categorías de LogManager registradas.                                                 | —              |
| **Select All**        | Muestra todas las categorías de registro en el visor inmediatamente.                                                                                                                                                                      | —              |
| **Deselect All**      | Oculta todas las categorías de registro del visor inmediatamente.                                                                                                                                                                        | —              |
| **Live / Paused**     | Cuando está en **Live**, el visor se desplaza automáticamente a la salida más reciente. Desplazarse hacia arriba cambia el estado a **Paused**. Hacer clic en el botón de alternancia cuando muestra **Paused** reanuda el desplazamiento automático y salta al final. | Live           |
| **Log path label**    | Muestra la ruta completa del archivo de registro que se está siguiendo.                                                                                                                                                                  | —              |
| **Close**             | Cierra el diálogo.                                                                                                                                                                                                                       | —              |

## Indicadores de Diagnóstico de Red

| Indicador | Descripción |
|---|---|
| **Status** | Calidad general del enlace: Excelente, Muy Buena, Buena, Aceptable o Malo (con código de colores verde → rojo). |
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
| **RX Buffer Now / Peak** | Llenado actual y máximo del buffer de audio en bytes y ms. |
| **Underruns (total / last sec)** | Contadores de subejecuciones de audio. |
| **Audio Arrival Gap / Max Arrival Gap** | Temporización de llegada entre paquetes. |
| **Network Jitter** | Estimación de jitter suavizada del flujo de audio en ms. |

## Consejos

- El diálogo Diagnóstico de Red respeta la configuración **FramelessWindow** de las preferencias de AetherSDR (`AppSettings > FramelessWindow`). Cuando está habilitada, el diálogo usa una geometría persistente que se guarda y restaura entre sesiones. Cuando está deshabilitada, el diálogo usa el marco de ventana estándar.
- La vista de registro se actualiza cada 500 ms, por lo que hay un breve retraso entre la escritura de un mensaje y su aparición en el visor.
- Los colores de resaltado de sintaxis ayudan a distinguir los niveles de registro de un vistazo: las líneas `INF` aparecen en azul, `WRN` en ámbar y `CRT`/`FTL` en rojo. Los nombres de las categorías se muestran en negrita. Los números y los tokens de protocolo (como `UDP`, `TCP`, `RX`, `TX`) se resaltan por separado.
- Si desea congelar la pantalla para leer una entrada específica, desplácese hacia arriba. El visor cambia automáticamente a **Paused**. Haga clic en **Live** para volver al seguimiento.
- Hacer clic en **Deselect All** y luego marcar una sola categoría es la forma más rápida de aislar la salida de un subsistema.

## Relacionados

- [Pausar el desplazamiento del registro para inspeccionar una entrada anterior](pause-log-scrolling-to-inspect-an-older-entry.md)
- [Descripción general de Diagnóstico de Red](overview.md)
- [Medir RTT y pérdida de paquetes durante problemas de audio](measure-rtt-and-packet-drops-during-audio-problems.md)
