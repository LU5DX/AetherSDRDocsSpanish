# Monitoree el audio de TX o RX en la visualización de forma de onda

El applet Waveform muestra una vista en vivo en el dominio del tiempo de la ruta de audio activa de TX o RX. Úselo para detectar recorte, pérdidas de señal y problemas de nivel de audio sin salir de la ventana principal.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere una conexión de radio; el applet muestra el audio del motor de audio local.
- El panel de applets debe estar visible. Si está oculto, actívelo mediante `View > Applet Panel`.

## Pasos

1. Localice el botón de bandeja WAVE en la fila superior de botones de bandeja de la barra lateral derecha.
2. Haga clic en WAVE para mostrar el applet Waveform. Haga clic nuevamente para ocultarlo.
3. Observe la visualización de la forma de onda. La traza se tiñe en tono frío cuando se monitorea audio de RX y en tono cálido cuando se monitorea audio de TX; no necesita leer etiquetas.
4. Verifique la lectura del encabezado para conocer la dirección actual (RX o TX), el nivel RMS en dBFS y el nivel pico en dBFS.
5. Si no ha llegado audio durante un segundo, la visualización muestra un mensaje de marcador de posición en lugar de una traza vacía. Para la ruta de RX, el mensaje dice **"no RX audio"**. Para la ruta de TX, dice **"no TX audio"**.
6. Para abrir el cajón de configuración, haga doble clic en cualquier parte de la visualización de la forma de onda. Haga doble clic nuevamente para cerrarlo. El estado abierto/cerrado del cajón se recuerda al reiniciar la aplicación.
7. En el cajón de configuración, use el cuadro combinado View para elegir una visualización: **Scope**, **Envelope**, **History** o **Bands**. El valor predeterminado es **Scope**.
8. Use el control deslizante Zoom para escalar el eje de amplitud. El valor predeterminado es 1.7x (rango 1.0x–6.0x). Arrastre hacia la derecha para ampliar señales pequeñas; con valores de zoom altos, los artefactos de recorte aparecen antes.
9. Use el control deslizante FPS para establecer la frecuencia con la que se repinta la visualización (rango 5–30 Hz, predeterminado 24). Los valores más bajos reducen la carga de la CPU.
10. Use el control deslizante Window para establecer la ventana de tiempo mostrada, en milisegundos (rango 10–500 ms, predeterminado 200 ms). La ventana de tiempo mostrada es continua; los valores más grandes muestran más historial con resolución reducida.

## Qué hace cada control

| Control                 | Predeterminado | Rango válido                                                     |
|-------------------------|----------------|------------------------------------------------------------------|
| View                    | Scope          | Scope, Envelope, History, Bands                                  |
| Zoom                    | 1.7x (170)     | 1.0x–6.0x (100–600)                                              |
| FPS                     | 24             | 5–30 Hz                                                          |
| Window                  | 200 ms         | 10–500 ms                                                        |
| Clic en la visualización | Live           | Live / Paused                                                    |
| Doble clic en la visualización | —       | —                                                                |
| Cajón de configuración  | Expandido      | Expandido / Colapsado                                            |

## Consejos

- Cuando ocurre recorte, las columnas afectadas se resaltan y aparece un contador CLIP N en el encabezado. Reduzca el nivel de excitación de audio o baje el valor de Zoom para que la señal vuelva a estar dentro del rango.
- Haga clic una vez en la forma de onda para congelar una instantánea cuando note una señal transitoria. Haga clic nuevamente para reanudar la vista en vivo.
- El cajón de configuración recuerda si estaba abierto o cerrado la última vez que lo usó y restaura ese estado en el siguiente inicio.
- El intervalo de discriminación de clic utilizado para detectar clic simple frente a doble clic se lee de la configuración de radio en el momento del clic, por lo que los cambios en `Settings > Radio Setup... > Audio > Click Discrimination Interval (ms)` surten efecto sin reiniciar AetherSDR.
- El control deslizante Window ofrece un ajuste continuo de 10 ms a 500 ms. La ventana predeterminada de 200 ms ofrece un buen equilibrio entre detalle e historial; los valores inferiores a 100 ms son útiles para detectar transitorios rápidos.
- Puede configurar los controles View, Zoom, FPS y Window mediante navegación por teclado. Cada control tiene un nombre accesible (WAVE view mode, WAVE zoom, WAVE FPS, WAVE window) que los lectores de pantalla pueden anunciar.

## Solución de problemas

- **La visualización muestra "no RX audio"** — No han llegado muestras de alcance de RX en el último segundo. Asegúrese de que PC Audio esté habilitado en la configuración de audio de la radio. Verifique que el dispositivo de audio correcto esté seleccionado en `Settings > Radio Setup...`.
- **La visualización muestra "no TX audio"** — No han llegado muestras de alcance de TX en el último segundo. Verifique que el audio fluya por la ruta de transmisión.
- **El botón de bandeja WAVE falta** — El panel de applets puede estar oculto. Actívelo mediante `View > Applet Panel`. Si el panel está visible pero WAVE no aparece, use `View > Reset Applet Order` para restaurar el diseño de applets predeterminado.
- **El clic simple y el doble clic no se distinguen de manera confiable** — Ajuste el intervalo de discriminación de clic en `Settings > Radio Setup... > Audio > Click Discrimination Interval (ms)`. Un intervalo más largo facilita los clics simples; un intervalo más corto facilita los dobles clics.

## Relacionado

- [Descripción general de Waveform](overview.md)
- [Pausar la forma de onda para inspeccionar una señal transitoria](pause-the-waveform-to-inspect-a-transient.md)
- [Cambiar el modo de vista de la forma de onda (Scope, Envelope, History, Bands)](switch-the-waveform-view-mode-scope-envelope-history-bands.md)
- [Ajustar el zoom de amplitud de la forma de onda](adjust-waveform-amplitude-zoom.md)
- [Establecer la frecuencia de actualización de la forma de onda para reducir la carga de la CPU](set-the-waveform-refresh-rate-to-reduce-cpu-load.md)
- Ajustar la ventana de tiempo de la forma de onda
