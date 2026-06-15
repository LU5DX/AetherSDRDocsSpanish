# Monitorear el audio de TX o RX en la visualización de forma de onda

El applet Waveform muestra una vista en vivo en el dominio del tiempo de la ruta de audio activa de TX o RX. Úselo para detectar recorte, pérdidas y problemas de nivel de audio sin salir de la ventana principal.

## Antes de comenzar

- AetherSDR debe estar ejecutándose. No se requiere una conexión de radio; el applet muestra el audio del motor de audio local.
- El panel de applets debe estar visible. Si está oculto, actívelo mediante `View > Applet Panel`.

## Pasos

1. Localice el botón de bandeja WAVE en la fila superior de botones de bandeja en la barra lateral derecha.
2. Haga clic en WAVE para mostrar el applet Waveform. Vuelva a hacer clic para ocultarlo.
3. Observe la visualización de la forma de onda. La traza se tiñe de color frío cuando monitorea audio de RX y de color cálido cuando monitorea audio de TX — no es necesario leer etiquetas.
4. Verifique la lectura del encabezado para ver la dirección actual (RX o TX), el nivel RMS en dBFS y el nivel pico en dBFS.
5. Si no ha llegado audio en un segundo, la pantalla muestra un mensaje de marcador de posición en lugar de una traza vacía. Para la ruta de RX, el mensaje dice **"no RX audio"**. Para la ruta de TX, dice **"no TX audio"**.
6. Para abrir el cajón de configuración, haga doble clic en cualquier lugar de la pantalla de forma de onda. Vuelva a hacer doble clic para cerrarlo. El estado abierto/cerrado del cajón se recuerda al reiniciar la aplicación.
7. En el cajón de configuración, use el cuadro combinado View para elegir una visualización: **Scope**, **Envelope**, **History** o **Bands**. El valor predeterminado es **Scope**.
8. Use el deslizador Zoom para escalar el eje de amplitud. El valor predeterminado es 1.7x (rango 1.0x–6.0x). Arrastre hacia la derecha para ampliar señales pequeñas; con valores de zoom altos, los artefactos de recorte aparecen antes.
9. Use el deslizador FPS para establecer la frecuencia con la que se vuelve a pintar la pantalla (rango 5–30 Hz, valor predeterminado 24). Los valores más bajos reducen la carga de la CPU.
10. Use el deslizador Window para establecer la ventana de tiempo mostrada. El deslizador se detiene en pasos discretos: 240 ms, 480 ms, 1 s, luego incrementos de 1 segundo hasta 10 s. El valor predeterminado es 1 s.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave persistida | Comportamiento |
|---|---|---|---|---|
| View | Scope | Scope, Envelope, History, Bands | `WaveApplet_ViewMode` | Selecciona el modo de visualización. Scope muestra la forma de onda mín/máx y líneas RMS. Envelope muestra un área rellena de pico/RMS. History muestra barras de nivel horizontales. Bands muestra barras de bandas de frecuencia. |
| Zoom | 1.7x (170) | 1.0x–6.0x (100–600) | `WaveApplet_ZoomPercent` | Escala verticalmente el eje de amplitud. |
| FPS | 24 | 5–30 Hz | `WaveApplet_RefreshRateHz` | Controla la frecuencia de repintado. |
| Window | 1 s | 240 ms, 480 ms, 1 s, 2 s, 3 s, 4 s, 5 s, 6 s, 7 s, 8 s, 9 s, 10 s | `WaveApplet_TimeWindowMs` | Establece la ventana de tiempo mostrada en intervalos de paso discretos. |
| Clic en la pantalla | En vivo | En vivo / En pausa | — | Alterna la pausa. Aparece una insignia PAUSED en el pie de página mientras la pantalla está congelada. El intervalo de discriminación de clic respeta el valor establecido en `Radio Setup > Audio > Click Discrimination Interval (ms)`. |
| Doble clic en la pantalla | — | — | — | Abre o cierra el cajón de configuración. |
| Cajón de configuración | Expandido | Expandido / Contraído | `WaveApplet_DrawerExpanded` | Recuerda el estado abierto/cerrado del cajón al reiniciar la aplicación. |

## Modo ligero

Cuando el applet está completamente oculto (no solo contraído en la bandeja, sino deshabilitado por el modo ligero de la aplicación), el applet Waveform entra en un estado de bajo consumo:

- El applet está oculto y no ocupa espacio en la interfaz de usuario.
- El controlador `appendScopeSamples` regresa inmediatamente sin procesar ningún dato de audio, por lo que el búfer de muestras nunca crece y el repintado de software de 24 Hz nunca se activa.
- La señal upstream `AudioEngine::{tx,rx}PostChainScopeReady` continúa activándose, pero el flujo de alcance se descarta en el hilo de la GUI.

Para activar o desactivar el modo ligero para el applet Waveform, use los controles de modo ligero de la aplicación. Cuando el modo ligero está activo, llamar a `setActive(false)` oculta el applet y evita todo el procesamiento de alcance. Llamar a `setActive(true)` restaura la visibilidad del applet y reanuda el procesamiento de audio.

## Consejos

- Cuando ocurre recorte, las columnas afectadas se resaltan y aparece un contador CLIP N en el encabezado. Reduzca su nivel de drive de audio o baje el valor de Zoom para que la señal vuelva a estar dentro del rango.
- Haga clic una vez en la forma de onda para congelar una instantánea cuando note un transitorio. Vuelva a hacer clic para reanudar la vista en vivo.
- El cajón de configuración recuerda si estaba abierto o cerrado la última vez que lo usó y restaura ese estado en el próximo inicio.
- El intervalo de discriminación de clic utilizado para la detección de clic simple versus doble clic se lee de la configuración de radio en el momento del clic, por lo que los cambios en `Settings > Radio Setup... > Audio > Click Discrimination Interval (ms)` surten efecto sin reiniciar AetherSDR.
- El deslizador Window usa pasos discretos en lugar de ajuste continuo. Cada muesca proporciona un valor de ventana de tiempo específico. Los primeros tres pasos (240 ms, 480 ms, 1 s) brindan detalle de subsegundo; los pasos restantes aumentan en incrementos de 1 segundo hasta 10 s.
- En el modo ligero, el applet está completamente inactivo — no consume ciclos de CPU para procesamiento de audio o repintado. Esto es más eficiente que simplemente ocultar el panel de applets.

## Solución de problemas

- **La pantalla muestra "no RX audio"** — No han llegado muestras de alcance de RX en el último segundo. Asegúrese de que PC Audio esté habilitado en la configuración de audio de la radio. Verifique que el dispositivo de audio correcto esté seleccionado en `Settings > Radio Setup...`.
- **La pantalla muestra "no TX audio"** — No han llegado muestras de alcance de TX en el último segundo. Verifique que el audio fluya a través de la ruta de transmisión.
- **Falta el botón de bandeja WAVE** — El panel de applets puede estar oculto. Actívelo mediante `View > Applet Panel`. Si el panel está visible pero falta WAVE, use `View > Reset Applet Order` para restaurar el diseño de applets predeterminado.
- **El clic simple y el doble clic no se distinguen de manera confiable** — Ajuste el intervalo de discriminación de clic en `Settings > Radio Setup... > Audio > Click Discrimination Interval (ms)`. Un intervalo más largo facilita los clics simples, un intervalo más corto facilita los dobles clics.
- **El applet no aparece y no se muestra ninguna forma de onda** — El applet puede estar deshabilitado por el modo ligero. Verifique la configuración del modo ligero de la aplicación para asegurarse de que el applet Waveform esté habilitado.

## Relacionado

- [Waveform overview](overview.md)
- [Pause the waveform to inspect a transient](pause-the-waveform-to-inspect-a-transient.md)
- [Switch the waveform view mode (Scope, Envelope, History, Bands)](switch-the-waveform-view-mode-scope-envelope-history-bands.md)
- [Adjust waveform amplitude zoom](adjust-waveform-amplitude-zoom.md)
- [Set the waveform refresh rate to reduce CPU load](set-the-waveform-refresh-rate-to-reduce-cpu-load.md)
- Adjust the waveform time window
