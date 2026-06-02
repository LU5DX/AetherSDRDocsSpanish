# Monitorizar audio de TX o RX en la visualización de la forma de onda

El applet Waveform muestra una vista en tiempo real del dominio temporal de la ruta de audio activa de TX o RX. Úselo para detectar recortes, pérdidas de audio y problemas de nivel de audio sin salir de la ventana principal.

## Antes de comenzar

- AetherSDR debe estar ejecutándose. No se requiere conexión de radio: el applet muestra el audio del motor de audio local.
- El panel de applets debe estar visible. Si está oculto, actívelo mediante `View > Applet Panel`.

## Pasos

1. Localice el botón de bandeja WAVE en la fila superior de botones de bandeja en la barra lateral derecha.
2. Haga clic en WAVE para mostrar el applet Waveform. Vuelva a hacer clic para ocultarlo.
3. Observe la visualización de la forma de onda. La traza se tiñe de color frío cuando se monitoriza audio de RX y de color cálido cuando se monitoriza audio de TX; no es necesario leer etiquetas.
4. Verifique la lectura del encabezado para conocer la dirección actual (RX o TX), el nivel RMS en dBFS y el nivel pico en dBFS.
5. Si no ha llegado audio en un segundo, la pantalla muestra un mensaje de marcador de posición en lugar de una traza vacía. Para la ruta de RX, el mensaje dice **"no RX audio"**. Para la ruta de TX, dice **"no TX audio"**.
6. Para abrir el cajón de configuraciones, haga doble clic en cualquier parte de la visualización de la forma de onda. Vuelva a hacer doble clic para cerrarlo. El estado abierto/cerrado del cajón se recuerda entre reinicios de la aplicación.
7. En el cajón de configuraciones, use el cuadro combinado View para elegir una visualización: **Scope**, **Envelope**, **History** o **Bands**. La opción predeterminada es **Scope**.
8. Use el deslizador Zoom para escalar el eje de amplitud. El valor predeterminado es 1.7x (rango 1.0x–6.0x). Arrastre hacia la derecha para ampliar señales pequeñas; con valores de zoom altos, los artefactos de recorte aparecen antes.
9. Use el deslizador FPS para establecer la frecuencia con la que se repinta la pantalla (rango 5–30 Hz, valor predeterminado 24). Los valores más bajos reducen la carga de la CPU.
10. Use el deslizador Window para configurar la ventana de tiempo mostrada. El deslizador se detiene en pasos discretos: 240 ms, 480 ms, 1 s, luego incrementos de 1 segundo hasta 10 s. El valor predeterminado es 1 s.

## Qué hace cada control

| Control | Predeterminado | Rango válido | Clave persistida | Comportamiento |
|---|---|---|---|---|
| View | Scope | Scope, Envelope, History, Bands | `WaveApplet_ViewMode` | Selecciona el modo de visualización. Scope muestra la forma de onda min/max y las líneas RMS. Envelope muestra un área rellena de pico/RMS. History muestra barras de nivel horizontales. Bands muestra barras de bandas de frecuencia. |
| Zoom | 1.7x (170) | 1.0x–6.0x (100–600) | `WaveApplet_ZoomPercent` | Escala verticalmente el eje de amplitud. |
| FPS | 24 | 5–30 Hz | `WaveApplet_RefreshRateHz` | Controla la frecuencia de repintado. |
| Window | 1 s | 240 ms, 480 ms, 1 s, 2 s, 3 s, 4 s, 5 s, 6 s, 7 s, 8 s, 9 s, 10 s | `WaveApplet_TimeWindowMs` | Establece la ventana de tiempo mostrada en intervalos discretos escalonados. |
| Clic en la pantalla | En vivo | En vivo / Pausado | — | Alterna la pausa. Aparece una insignia PAUSED en el pie de página mientras la pantalla está congelada. El intervalo de discriminación de clic respeta el valor establecido en `Radio Setup > Audio > Click Discrimination Interval (ms)`. |
| Doble clic en la pantalla | — | — | — | Alterna la apertura o cierre del cajón de configuraciones. |
| Cajón de configuraciones | Expandido | Expandido / Contraído | `WaveApplet_DrawerExpanded` | Recuerda el estado abierto/cerrado del cajón entre reinicios de la aplicación. |

## Consejos

- Cuando se produce recorte, las columnas afectadas se resaltan y aparece un contador CLIP N en el encabezado. Reduzca su nivel de audio de entrada o disminuya el valor de Zoom para que la señal vuelva al rango.
- Haga clic una vez en la forma de onda para congelar una instantánea cuando note una transitoria. Vuelva a hacer clic para reanudar la vista en vivo.
- El cajón de configuraciones recuerda si estaba abierto o cerrado la última vez que lo usó y restaura ese estado en el siguiente inicio.
- El intervalo de discriminación de clic utilizado para la detección de clic simple versus doble clic se lee de la configuración de radio en el momento del clic, por lo que los cambios en `Settings > Radio Setup... > Audio > Click Discrimination Interval (ms)` surten efecto sin reiniciar AetherSDR.
- El deslizador Window utiliza pasos discretos en lugar de ajuste continuo. Cada muesca proporciona un valor específico de ventana de tiempo. Los primeros tres pasos (240 ms, 480 ms, 1 s) ofrecen detalle de subsegundo; los pasos restantes aumentan en incrementos de 1 segundo hasta 10 s.

## Solución de problemas

- **La pantalla muestra "no RX audio"** — No han llegado muestras de alcance de RX en el último segundo. Asegúrese de que PC Audio esté habilitado en la configuración de audio de la radio. Verifique que el dispositivo de audio correcto esté seleccionado en `Settings > Radio Setup...`.
- **La pantalla muestra "no TX audio"** — No han llegado muestras de alcance de TX en el último segundo. Verifique que el audio fluya a través de la ruta de transmisión.
- **Falta el botón de bandeja WAVE** — El panel de applets puede estar oculto. Actívelo mediante `View > Applet Panel`. Si el panel está visible pero WAVE no aparece, use `View > Reset Applet Order` para restaurar el diseño de applets predeterminado.
- **El clic simple y el doble clic no se distinguen de forma fiable** — Ajuste el intervalo de discriminación de clic en `Settings > Radio Setup... > Audio > Click Discrimination Interval (ms)`. Un intervalo más largo facilita los clics simples; un intervalo más corto facilita los dobles clics.

## Relacionado

- [Waveform overview](overview.md)
- [Pause the waveform to inspect a transient](pause-the-waveform-to-inspect-a-transient.md)
- [Switch the waveform view mode (Scope, Envelope, History, Bands)](switch-the-waveform-view-mode-scope-envelope-history-bands.md)
- [Adjust waveform amplitude zoom](adjust-waveform-amplitude-zoom.md)
- [Set the waveform refresh rate to reduce CPU load](set-the-waveform-refresh-rate-to-reduce-cpu-load.md)
- [Ajuste la ventana de tiempo de la forma de onda](adjust-the-waveform-time-window.md)
