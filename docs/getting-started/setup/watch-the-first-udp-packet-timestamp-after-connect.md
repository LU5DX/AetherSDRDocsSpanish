# Observar la marca de tiempo del primer paquete UDP tras la conexión

Use el diálogo de Diagnóstico de Red para confirmar que el flujo de datos UDP de la radio ha llegado a su equipo después de conectarse. El indicador **First UDP Packet** le indica si ha llegado algún tráfico UDP desde que comenzó la sesión actual.

## Antes de empezar

- AetherSDR debe estar en ejecución. El diálogo puede abrirse tanto si hay una radio conectada como si no, pero **First UDP Packet** solo tiene sentido después de un intento de conexión.
- Ya debe haber iniciado una conexión a una radio FLEX-8600.

## Pasos

1. Haga clic en `Settings > Network...`.
2. En el diálogo **Network Diagnostics**, localice el grupo **Network Status**.
3. Lea el indicador **First UDP Packet**. Muestra `Yes` si se ha recibido al menos un paquete UDP desde la conexión, o `No` si aún no ha llegado ninguno.
4. Haga clic en `Close` para cerrar el diálogo.

## Qué hace cada control

| Indicador / Control        | Significado o Comportamiento                                                                                                                                                | Notas                                                                             |
|----------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------|
| **First UDP Packet**       | Muestra `Yes` o `No`. Se actualiza una vez por segundo. Indica si se ha recibido algún paquete UDP de la radio en la sesión actual.                                          |                                                                                   |
| **Status**                 | Calidad general del enlace, codificada por colores de verde a rojo. Estados: Excellent, Very Good, Good, Fair, Poor.                                                         |                                                                                   |
| **Local UDP**              | El extremo local UDP en el que AetherSDR está escuchando. Útil para confirmar que el puerto correcto está enlazado.                                                          |                                                                                   |
| **Local TCP**              | El extremo local TCP en uso para la conexión actual.                                                                                                                         |                                                                                   |
| **Target Radio IP**        | Dirección IP de la radio conectada, o "Not connected".                                                                                                                      |                                                                                   |
| **Selected Source**        | NIC local o ruta de enlace utilizada para la conexión.                                                                                                                       |                                                                                   |
| **Latency (RTT)**          | Tiempo de ida y vuelta actual.                                                                                                                                              |                                                                                   |
| **Max Latency (RTT)**      | RTT más alto observado desde la conexión.                                                                                                                                   |                                                                                   |
| **Network Jitter**         | Estimación de fluctuación suavizada del flujo de audio en ms.                                                                                                                |                                                                                   |
| **Audio / FFT / Waterfall / Meters / DAX rates** | Tasa de ingreso por categoría en kbps.                                                                                                   |                                                                                   |
| **Total RX / Total TX**    | Bytes agregados por segundo en cada dirección.                                                                                                                              |                                                                                   |
| **Audio / FFT / Waterfall / Meters / DAX drops** | Conteo de paquetes perdidos por categoría y porcentaje.                                                                                           |                                                                                   |
| **RX Buffer Now / Peak**   | Llenado actual y máximo del búfer de audio en bytes y ms.                                                                                                                   |                                                                                   |
| **Underruns (total / last sec)** | Contadores de subejecución de audio.                                                                                                                                 |                                                                                   |
| **Audio Arrival Gap / Max Arrival Gap** | Temporización entre llegadas de paquetes.                                                                                                                    |                                                                                   |
| **Log path label**         | Muestra la ruta completa del archivo de registro que se está siguiendo en la pestaña Logs.                                                                                   |                                                                                   |
| Overview (pestaña)         | Muestra cuatro tarjetas de estado (Status, Latency, Packet Loss, Audio Buffer) y cuatro gráficos de series temporales (Latency and Jitter, Recent Packet Loss, Total Stream Rates, Audio Buffer). |                                                                                   |
| Details (pestaña)          | Cuadrícula desplazable con valores etiquetados para los grupos Network Status, Incoming Stream Rates, Packet Loss y Audio Playback.                                          |                                                                                   |
| Latency (pestaña)          | Gráfico de series temporales de ancho completo de RTT, intervalo de llegada y fluctuación en ms.                                                                              |                                                                                   |
| Rates (pestaña)            | Gráfico de series temporales de ancho completo con escala logarítmica de las tasas de bits entrantes por flujo (RX total, Audio, FFT, Waterfall, Meters, DAX) en kbps.       |                                                                                   |
| Packet Loss (pestaña)      | Gráfico de series temporales de ancho completo del porcentaje de pérdida de paquetes por categoría de flujo.                                                                |                                                                                   |
| Audio (pestaña)            | Gráfico de series temporales de ancho completo del llenado del búfer de reproducción (ms) y subejecuciones/s.                                                               |                                                                                   |
| Logs (pestaña)             | Seguimiento en vivo del archivo de registro de AetherSDR, filtrado por casillas de verificación de categoría. Resaltado de sintaxis por nivel de registro y nombre de categoría. | El selector de Timeframe está oculto mientras esta pestaña esté activa.           |
| Timeframe                  | Seleccina cuánto tiempo atrás muestran el historial los gráficos de series temporales. El valor predeterminado es 5 minutos. Opciones: 1 minute, 5 minutes, 15 minutes, 1 hour, 1 day, 1 week. | Se muestra en la esquina superior derecha de la barra de pestañas; oculto cuando la pestaña Logs está activa. |
| Filter Categories (Logs)   | Casillas de verificación por categoría que filtran la vista de registro. Incluye la categoría General (predeterminada) más todas las categorías registradas de LogManager. |                                                                                   |
| Select All (Logs)          | Muestra todas las categorías de registro en el visor.                                                                                                                       |                                                                                   |
| Deselect All (Logs)        | Oculta todas las categorías de registro del visor.                                                                                                                          |                                                                                   |
| Live / Paused (Logs)       | En modo Live, el visor se desplaza automáticamente a la salida más reciente. Al desplazarse hacia arriba se pausa automáticamente; al hacer clic en Live se reanuda y salta al final. |                                                                                   |
| Close                      | Cierra el diálogo.                                                                                                                                                          |                                                                                   |

## Uso de la pestaña Logs

La pestaña **Logs** proporciona un seguimiento en vivo del archivo de registro de AetherSDR directamente dentro del diálogo.

1. Haga clic en la pestaña **Logs**.
2. La ruta completa del archivo de registro que se está siguiendo se muestra en la parte superior de la pestaña en el **Log path label**.
3. Use las casillas de verificación **Filter Categories** para mostrar solo las categorías que le interesen. La categoría **General** está disponible de forma predeterminada; las categorías adicionales reflejan todas las categorías registradas de LogManager.
4. Haga clic en **Select All** para habilitar todas las categorías a la vez, o en **Deselect All** para limpiar todas las selecciones.
5. El visor comienza en modo **Live** y se desplaza automáticamente a la salida más reciente. Desplácese hacia arriba en cualquier momento para pausar el desplazamiento automático; el interruptor cambia a **Paused**.
6. Haga clic en **Live** para reanudar el desplazamiento automático y volver al final.

Las entradas de registro se resaltan por sintaxis según el nivel de registro (DBG, INF, WRN, CRT/FTL) y por nombre de categoría, marcas de tiempo, valores numéricos y palabras clave de protocolo.

> **Nota:** El selector **Timeframe** está oculto mientras la pestaña Logs esté activa. Cambie a cualquier otra pestaña para restaurarlo.

## Consejos

- El diálogo actualiza todos los indicadores una vez por segundo. Si **First UDP Packet** permanece en `No` durante varios segundos después de la conexión, el tráfico UDP no está llegando al anfitrión: verifique las reglas del cortafuegos, el enrutamiento y que el extremo UDP local mostrado en **Local UDP** sea accesible desde la radio.
- En una VPN o un enlace enrutado, TCP puede conectarse con éxito mientras que UDP está bloqueado por separado. Que **First UDP Packet** muestre `No` con **Status** mostrando un estado conectado es una señal fiable de esta división.
- **First UDP Packet** se reinicia en cada nueva conexión. Desconéctese y vuelva a conectarse si desea volver a verificar la entrega después de cambiar la configuración de red.
- Use el selector **Timeframe** para reducir o ampliar el historial mostrado en todas las pestañas de series temporales. El valor predeterminado es 5 minutos.
- La pestaña **Rates** utiliza una escala logarítmica para que los flujos de baja tasa de bits (como Meters) sigan siendo visibles junto con el total de RX de mayor tasa de bits.
- El diálogo utiliza una ventana sin marco de forma predeterminada. Se puede activar o desactivar mediante la configuración global `FramelessWindow`. Cuando el modo sin marco está activo, aparece una barra de título en la parte superior del diálogo para arrastrar y cerrar. Cuando el modo sin marco está desactivado, se muestra el marco de ventana estándar del sistema operativo.

## Solución de problemas

- **First UDP Packet se queda en "No" después de la conexión** — El UDP no está llegando al extremo local. Verifique que ningún cortafuegos esté bloqueando UDP en el puerto mostrado en **Local UDP**, y que la radio pueda enrutar de vuelta a la IP de su equipo. En una conexión VPN, confirme que la VPN pase UDP en ambos sentidos.
- **First UDP Packet muestra "Yes" pero no hay audio** — El UDP está llegando, pero un problema diferente afecta la reproducción. Revise el grupo **Audio Playback** en la pestaña Details en busca de subejecuciones o problemas de búfer, y consulte la página de diagnóstico de audio.
- **El visor de registro está vacío o no muestra entradas** — Confirme que al menos una casilla de verificación de **Filter Categories** esté seleccionada. Si todas las categorías están deseleccionadas, no se muestran entradas. Haga clic en **Select All** para restaurar la visibilidad.

## Relacionado

- [Network Diagnostics overview](../../features/network-diagnostics/overview.md)
- [Verify the radio's IP and local bind address](../../features/network-diagnostics/verify-the-radio-s-ip-and-local-bind-address.md)
- [Measure RTT and packet drops during audio problems](../../features/network-diagnostics/measure-rtt-and-packet-drops-during-audio-problems.md)
- [Diagnose audio underruns and jitter](../../troubleshooting/networkdiagnostics/diagnose-audio-underruns-and-jitter.md)
- [Connect by IP across a VPN or routed network](connect-by-ip-across-a-vpn-or-routed-network.md)
- [Pick the local network interface used for a manual connection](pick-the-local-network-interface-used-for-a-manual-connection.md)
