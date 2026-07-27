# Monitorear el audio de TX o RX en la visualización de forma de onda

El applet de forma de onda muestra una vista en vivo en el dominio del tiempo de la ruta de audio activa de TX o RX. Úselo para detectar recorte, pérdidas y problemas de nivel de audio sin salir de la ventana principal.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere una conexión de radio; el applet muestra el audio del motor de audio local.
- El panel de applets debe estar visible. Si está oculto, actívelo mediante `View > Applet Panel`.

## Pasos

1. Localice el botón de la bandeja WAVE en la fila superior de botones de la bandeja en la barra lateral derecha.
2. Haga clic en WAVE para mostrar el applet de forma de onda. Vuelva a hacer clic para ocultarlo.
3. Observe la visualización de la forma de onda. La traza se tiñe de color frío cuando monitorea audio de RX y de color cálido cuando monitorea audio de TX, sin necesidad de leer etiquetas.
4. Verifique la lectura del encabezado para conocer la dirección actual (RX o TX), el nivel RMS en dBFS y el nivel pico en dBFS.
5. Si no ha llegado audio durante un segundo, la pantalla muestra un mensaje de marcador de posición en lugar de una traza vacía. Para la ruta RX, el mensaje dice **"no RX audio"**. Para la ruta TX, dice **"no TX audio"**.
6. Para abrir el cajón de configuración, haga doble clic en cualquier lugar de la visualización de forma de onda. Vuelva a hacer doble clic para cerrarlo. El estado abierto/cerrado del cajón se recuerda entre reinicios de la aplicación.
7. En el cajón de configuración, use el cuadro combinado View para elegir una visualización: **Scope**, **Envelope**, **History** o **Bands**. El valor predeterminado es **Scope**.
8. Use el control deslizante Zoom para escalar el eje de amplitud. El valor predeterminado es 1.7x (rango 1.0x–6.0x). Arrastre hacia la derecha para ampliar señales pequeñas; con valores altos de zoom, los artefactos de recorte aparecen antes.
9. Use el control deslizante FPS para establecer la frecuencia con la que se vuelve a pintar la pantalla (rango 5–60 Hz, valor predeterminado 25). Los valores más bajos reducen la carga de la CPU.
10. Use el control deslizante Window para establecer la ventana de tiempo mostrada. El control deslizante se detiene en pasos discretos: 240 ms, 480 ms, 1 s, luego incrementos de 1 segundo hasta 10 s. El valor predeterminado es 1 s.

## Qué hace cada control

| Control                 | Predeterminado | Rango válido                                                       |
|-------------------------|----------------|--------------------------------------------------------------------|
| View                    | Scope          | Scope, Envelope, History, Bands                                    |
| Zoom                    | 1.7x (170)     | 1.0x–6.0x (100–600)                                                |
| FPS                     | 25             | 5–60 Hz                                                            |
| Window                  | 1 s            | 240 ms, 480 ms, 1 s, 2 s, 3 s, 4 s, 5 s, 6 s, 7 s, 8 s, 9 s, 10 s |
| Clic en la pantalla     | En vivo        | En vivo / Pausado                                                  |
| Doble clic en la pantalla | —            | —                                                                  |
| Cajón de configuración  | Expandido      | Expandido / Colapsado                                              |

## Consejos

- Cuando ocurre recorte, las columnas afectadas se resaltan y aparece un contador CLIP N en el encabezado. Reduzca su nivel de excitación de audio o disminuya el valor de Zoom para que la señal vuelva a estar dentro del rango.
- Haga clic una vez en la forma de onda para congelar una instantánea cuando note un transitorio. Vuelva a hacer clic para reanudar la vista en vivo.
- El cajón de configuración recuerda si estaba abierto o cerrado la última vez que lo usó y restaura ese estado en el próximo inicio.
- El intervalo de discriminación de clic utilizado para la detección de un solo clic frente a doble clic se lee de la configuración de radio en el momento del clic, por lo que los cambios en `Settings > Radio Setup... > Audio > Click Discrimination Interval (ms)` surten efecto sin reiniciar AetherSDR.
- El control deslizante Window utiliza pasos discretos en lugar de ajuste continuo. Cada muesca proporciona un valor de ventana de tiempo específico. Los primeros tres pasos (240 ms, 480 ms, 1 s) brindan detalle de subsegundo; los pasos restantes aumentan en incrementos de 1 segundo hasta 10 s.
- Puede configurar los controles View, Zoom, FPS y Window mediante la navegación con el teclado. Cada control tiene un nombre accesible (WAVE view mode, WAVE zoom, WAVE FPS, WAVE window) que los lectores de pantalla pueden anunciar.

## Solución de problemas

- **La pantalla muestra "no RX audio"** — No han llegado muestras de alcance de RX en el último segundo. Asegúrese de que PC Audio esté habilitado en la configuración de audio de la radio. Verifique que el dispositivo de audio correcto esté seleccionado en `Settings > Radio Setup...`.
- **La pantalla muestra "no TX audio"** — No han llegado muestras de alcance de TX en el último segundo. Verifique que el audio fluya a través de la ruta de transmisión.
- **Falta el botón de la bandeja WAVE** — El panel de applets puede estar oculto. Actívelo mediante `View > Applet Panel`. Si el panel está visible pero WAVE está ausente, use `View > Reset Applet Order` para restaurar la disposición predeterminada de applets.
- **No se distinguen de manera confiable el clic simple y el doble clic** — Ajuste el intervalo de discriminación de clic en `Settings > Radio Setup... > Audio > Click Discrimination Interval (ms)`. Un intervalo más largo facilita los clics simples; un intervalo más corto facilita los dobles clics.

## Relacionado

- [Waveform overview](overview.md)
- [Pause the waveform to inspect a transient](pause-the-waveform-to-inspect-a-transient.md)
- [Switch the waveform view mode (Scope, Envelope, History, Bands)](switch-the-waveform-view-mode-scope-envelope-history-bands.md)
- [Adjust waveform amplitude zoom](adjust-waveform-amplitude-zoom.md)
- [Set the waveform refresh rate to reduce CPU load](set-the-waveform-refresh-rate-to-reduce-cpu-load.md)
- Adjust the waveform time window
