# Diagnóstico de Red

El cuadro de diálogo de Diagnóstico de Red ofrece una vista en vivo del enlace de red con la radio. Dispone de un diseño con múltiples pestañas que incluye un panel de resumen, métricas detalladas, gráficos de rendimiento por flujo y un visor de registros en vivo.

## Cómo abrir el Diagnóstico de Red

1. Vaya a `Settings > Network...`.
2. Se abrirá el cuadro de diálogo de Diagnóstico de Red.

## Pestañas

El cuadro de diálogo contiene las siguientes pestañas:

- **Overview** – Muestra cuatro tarjetas de estado (Estado, Latencia, Pérdida de Paquetes, Búfer de Audio) y cuatro gráficos de series temporales (Latencia y Jitter, Pérdida de Paquetes Reciente, Tasas Totales de Flujo, Búfer de Audio).
- **Details** – Una cuadrícula desplazable con valores etiquetados para los grupos de Estado de Red, Tasas de Flujo Entrante, Pérdida de Paquetes y Reproducción de Audio.
- **Latency** – Gráfico de series temporales de ancho completo del RTT, intervalo de llegada y jitter en ms.
- **Rates** – Gráfico de series temporales de ancho completo con escala logarítmica de las tasas de bits entrantes por flujo (RX total, Audio, FFT, Waterfall, Medidores, DAX) en kbps.
- **Packet Loss** – Gráfico de series temporales de ancho completo del porcentaje de pérdida de paquetes por categoría de flujo.
- **Audio** – Gráfico de series temporales de ancho completo del llenado del búfer de reproducción (ms) y de las subcargas por segundo. Incluye diagnósticos de audio RX por flujo que muestran la tasa de alimentación, déficit, paquetes tardíos, código de clase de paquete y estado del flujo para cada flujo de audio activo.
- **Logs** – Visualización en vivo del archivo de registro de AetherSDR, filtrada por casillas de verificación de categoría. Con resaltado de sintaxis por nivel de registro y nombre de categoría. El selector de intervalo de tiempo se oculta mientras esta pestaña está activa.

## Selector de intervalo de tiempo

Un menú desplegable en la esquina superior derecha de la barra de pestañas selecciona hasta qué punto del pasado muestran los gráficos de series temporales. Las siguientes opciones están disponibles:

- 1 minuto
- 5 minutos (predeterminado)
- 15 minutos
- 30 minutos
- 1 hora
- 1 día
- 1 semana

El selector de intervalo de tiempo se oculta cuando la pestaña **Logs** está activa.

## Pausar el desplazamiento de registros para inspeccionar una entrada anterior

La pestaña Logs sigue el archivo de registro de AetherSDR en tiempo real. Esta sección explica cómo pausar ese desplazamiento automático para poder leer una entrada anterior sin que se mueva, y cómo reanudar la visualización en vivo cuando haya terminado.

### Pasos

1. Abra el Diagnóstico de Red mediante `Settings > Network...`.
2. Haga clic en la pestaña **Logs**.
3. Para pausar el desplazamiento, realice una de las siguientes acciones:
   - Desplácese hacia arriba en el visor de registros. El visor cambia automáticamente al estado **Paused**.
   - Haga clic en el botón de alternancia, que muestra **Live**, para cambiarlo a **Paused**.
4. Lea la entrada que necesite. La pantalla permanece fija mientras el botón muestra **Paused**.
5. Cuando esté listo para volver a la visualización en vivo, haga clic en el botón de alternancia, que ahora muestra **Paused**, para cambiarlo de nuevo a **Live**. El visor salta inmediatamente a la salida más reciente y reanuda el desplazamiento automático.

### Controles de la pestaña Logs

| Control                            | Predeterminado | Comportamiento                                                                                                                                                                                                                                                                                                                                              |
|------------------------------------|----------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Live / Paused** (botón de alternancia) | Live           | Cuando está en **Live**, el visor se desplaza automáticamente a la salida de registro más reciente. Cuando está en **Paused**, el desplazamiento se detiene y la pantalla mantiene su posición actual. Desplazarse hacia arriba en el visor cambia automáticamente el botón a **Paused**. Al hacer clic en el botón mientras muestra **Paused** se reanuda el desplazamiento automático y se salta al final. |
| **Filter Categories** (casillas de verificación) | –              | Las casillas de verificación por categoría filtran la vista de registro. Incluye una categoría "General" (predeterminada) más todas las categorías registradas de LogManager.                                                                                                                                                                             |
| **Select All** (botón pulsador)    | –              | Muestra todas las categorías de registro en el visor.                                                                                                                                                                                                                                                                                                      |
| **Deselect All** (botón pulsador)  | –              | Oculta todas las categorías de registro del visor.                                                                                                                                                                                                                                                                                                         |

### Consejos

- Desplazarse hacia arriba es la forma más rápida de pausar: no necesita alcanzar primero el botón de alternancia.
- La vista de registro tiene resaltado de sintaxis por nivel de registro y nombre de categoría, lo que facilita encontrar la entrada que busca.
- Las casillas de verificación de filtro de categoría y los botones **Select All** y **Deselect All** permanecen activos mientras está en pausa, por lo que puede reducir las entradas visibles sin reanudar el desplazamiento en vivo.

## Indicadores

El cuadro de diálogo muestra los siguientes indicadores:

| Indicador | Significado |
|---|---|
| Estado | Calidad general del enlace, codificada por colores verde → rojo. Estados: Excelente, Muy Buena, Buena, Aceptable, Mala |
| IP de la Radio de Destino | IP de la radio conectada, o "No conectada" |
| Fuente Seleccionada | NIC local/ruta de enlace utilizada para la conexión |
| TCP Local | Extremo TCP local |
| UDP Local | Extremo UDP local |
| Primer Paquete UDP | Si se ha recibido el primer paquete UDP desde la conexión (Sí/No) |
| Latencia (RTT) | Tiempo de ida y vuelta actual |
| Latencia Máx. (RTT) | RTT más alto observado desde la conexión |
| Tasas de Audio / FFT / Waterfall / Medidores / DAX | Tasa de ingreso por categoría en kbps |
| RX Total / TX Total | Bytes agregados por segundo en cada dirección |
| Pérdidas de Audio / FFT / Waterfall / Medidores / DAX | Conteos y porcentaje de paquetes perdidos por categoría |
| Búfer RX Ahora / Máximo | Llenado actual y máximo del búfer de audio en bytes y ms |
| Subcargas (total / último segundo) | Contadores de subcargas de audio |
| Intervalo de Llegada de Audio / Intervalo de Llegada Máx. | Temporización de llegada entre paquetes |
| Jitter de Red | Estimación suavizada del jitter del flujo de audio en ms |
| Etiqueta de ruta de registro | Ruta completa del archivo de registro que se está siguiendo |

## Cerrar el cuadro de diálogo

Haga clic en **Close** para cerrar el cuadro de diálogo de Diagnóstico de Red.
