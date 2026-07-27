# Ver salida de registro en vivo filtrada por categoría de diagnóstico

La pestaña Registros en Diagnóstico de Red muestra un seguimiento en vivo del archivo de registro de AetherSDR, filtrado solo por las categorías de diagnóstico que usted elija. Úselo cuando necesite observar mensajes específicos de un subsistema en tiempo real sin tener que revisar información no relacionada.

## Antes de comenzar

- AetherSDR debe estar ejecutándose. No se requiere una conexión de radio para ver el registro.
- Sepa qué categoría de diagnóstico desea observar (por ejemplo, `aether.connection`, `aether.cw`, `aether.dxcluster`).

## Pasos

1. Haga clic en `Settings > Network...` para abrir el diálogo de Diagnóstico de Red.
2. Haga clic en la pestaña **Logs**.
3. Revise la ruta del registro mostrada en la **etiqueta de ruta del registro** en la parte superior de la pestaña para confirmar qué archivo se está rastreando.
4. Marque o desmarque las casillas por categoría en **Filter Categories** para mostrar solo las categorías que desee. De forma predeterminada, la categoría **General** está disponible; todas las categorías de diagnóstico registradas aparecen junto a ella.
5. Para mostrar todas las categorías a la vez, haga clic en **Select All**. Para ocultar todas las categorías, haga clic en **Deselect All**, luego marque solo las categorías específicas que necesite.
6. Observe el visor. Las nuevas entradas se desplazan automáticamente mientras el selector muestra **Live**.
7. Cuando termine, haga clic en **Close**.

## Función de cada control

| Control                | Comportamiento                                                                                                                                                                                                                                                                                   | Predeterminado |
|------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------|
| **Overview** (pestaña) | Muestra cuatro tarjetas de estado (Estado, Latencia, Pérdida de paquetes, Búfer de audio) y cuatro gráficos de series temporales (Latencia y Jitter, Pérdida de paquetes reciente, Tasas de flujo totales, Búfer de audio).                                                                       | —              |
| **Details** (pestaña)   | Cuadrícula desplazable con valores etiquetados para los grupos de Estado de red, Tasas de flujo entrante, Pérdida de paquetes y Reproducción de audio.                                                                                                                                           | —              |
| **Latency** (pestaña)   | Gráfico de series temporales de ancho completo de RTT, intervalo de llegada y jitter en ms.                                                                                                                                                                                                      | —              |
| **Rates** (pestaña)     | Gráfico de series temporales de ancho completo y escala logarítmica de las tasas de bits entrantes por flujo (RX total, Audio, FFT, Waterfall, Medidores, DAX) en kbps.                                                                                                                           | —              |
| **Packet Loss** (pestaña) | Gráfico de series temporales de ancho completo del porcentaje de pérdida de paquetes por categoría de flujo.                                                                                                                                                                                     | —              |
| **Audio** (pestaña)     | Gráfico de series temporales de ancho completo del llenado del búfer de reproducción (ms) y subtasa/segundo. Incluye diagnóstico de audio RX por flujo que muestra la tasa de alimentación, déficit, paquetes tardíos, código de clase de paquete y salud del flujo para cada flujo de audio activo. | —              |
| **Logs** (pestaña)      | Seguimiento en vivo del archivo de registro de AetherSDR filtrado por las casillas de categoría. Resaltado de sintaxis por nivel de registro y nombre de categoría. El selector **Timeframe** está oculto mientras esta pestaña está activa.                                                       | —              |
| **Timeframe**           | Selecciona cuánto tiempo atrás muestran el historial los gráficos de series temporales. Oculto cuando la pestaña Registros está activa.                                                                                                                                                           | 5 minutos      |
| **Filter Categories**   | Casillas de verificación por categoría. Marque una categoría para incluir sus líneas; desmárquela para ocultarlas. Incluye **General** más todas las categorías de LogManager registradas.                                                                                                        | —              |
| **Select All**          | Muestra inmediatamente todas las categorías de registro en el visor.                                                                                                                                                                                                                             | —              |
| **Deselect All**        | Oculta inmediatamente todas las categorías de registro del visor.                                                                                                                                                                                                                                | —              |
| **Live / Paused**       | Cuando está en **Live**, el visor se desplaza automáticamente a la salida más reciente. Desplazarse hacia arriba cambia el estado a **Paused**. Al hacer clic en el selector cuando muestra **Paused** se reanuda el desplazamiento automático y salta al final.                                  | Live           |
| **Log path label**      | Muestra la ruta completa del sistema de archivos del archivo de registro que se está rastreando.                                                                                                                                                                                                | —              |
| **Close**               | Cierra el diálogo.                                                                                                                                                                                                                                                                               | —              |

## Indicadores de Diagnóstico de Red

| Indicador | Descripción |
|---|---|
| **Status** | Calidad general del enlace: Excelente, Muy buena, Buena, Aceptable o Mala (codificado por colores verde → rojo). |
| **Target Radio IP** | IP de la radio conectada, o 'No conectado'. |
| **Selected Source** | NIC/ruta de enlace local utilizada para la conexión. |
| **Local TCP** | Punto final TCP local. |
| **Local UDP** | Punto final UDP local. |
| **First UDP Packet** | Si se ha recibido el primer paquete UDP desde la conexión (Sí/No). |
| **Latency (RTT)** | Tiempo de ida y vuelta actual. |
| **Max Latency (RTT)** | RTT más alto observado desde la conexión. |
| **Tasas Audio / FFT / Waterfall / Meters / DAX** | Tasa de ingreso por categoría en kbps. |
| **Total RX / Total TX** | Bytes agregados por segundo en cada dirección. |
| **Pérdidas Audio / FFT / Waterfall / Meters / DAX** | Conteos y porcentajes de paquetes perdidos por categoría. |
| **RX Buffer Ahora / Pico** | Llenado actual y máximo del búfer de audio en bytes y ms. |
| **Subtasa (total / último segundo)** | Contadores de subtasa de audio. |
| **Intervalo de llegada de audio / Intervalo de llegada máximo** | Tiempo de llegada entre paquetes. |
| **Jitter de red** | Estimación de jitter suavizado del flujo de audio en ms. |

## Consejos

- El diálogo de Diagnóstico de Red respeta la configuración **FramelessWindow** de las preferencias de AetherSDR (`AppSettings > FramelessWindow`). Cuando está habilitada, el diálogo usa una geometría persistente que se guarda y restaura entre sesiones. Cuando está deshabilitada, el diálogo usa el marco de ventana estándar.
- La vista de registro se actualiza cada 500 ms, por lo que hay un breve retraso entre la escritura de un mensaje y su aparición en el visor.
- Los colores de resaltado de sintaxis ayudan a distinguir los niveles de registro de un vistazo: las líneas `INF` aparecen en azul, `WRN` en ámbar y `CRT`/`FTL` en rojo. Los nombres de las categorías se muestran en negrita. Los números y tokens de protocolo (como `UDP`, `TCP`, `RX`, `TX`) se resaltan por separado.
- Si desea congelar la pantalla para leer una entrada específica, desplácese hacia arriba. El visor cambia automáticamente a **Paused**. Haga clic en **Live** para volver al final del registro.
- Hacer clic en **Deselect All** y luego marcar una sola categoría es la forma más rápida de aislar la salida de un subsistema.
- En la versión v26.7.4, el diálogo usa un árbol de navegación a la izquierda y un panel de contenido a la derecha. Haga clic en un nombre de página en el árbol **Network Diagnostics Navigation** para cambiar entre páginas. Un campo de búsqueda en la parte superior del árbol de navegación le permite filtrar las páginas disponibles por nombre.

## Relacionados

- [Pausar el desplazamiento del registro para inspeccionar una entrada anterior](pause-log-scrolling-to-inspect-an-older-entry.md)
- [Descripción general de Diagnóstico de Red](overview.md)
- [Medir RTT y pérdida de paquetes durante problemas de audio](measure-rtt-and-packet-drops-during-audio-problems.md)
