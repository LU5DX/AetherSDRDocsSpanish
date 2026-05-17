# Monitorizar audio de TX o RX en la visualización de forma de onda

El applet Waveform muestra una vista en tiempo real del dominio temporal de la ruta de audio activa de TX o RX. Úselo para detectar recorte, pérdidas y problemas de nivel de audio sin salir de la ventana principal.

## Antes de empezar

- AetherSDR debe estar ejecutándose. No se requiere conexión de radio: el applet muestra el audio del motor de audio local.
- El panel de applets debe estar visible. Si está oculto, actívelo mediante `View > Applet Panel`.

## Pasos

1. Localice el botón de bandeja WAVE en la fila superior de botones de bandeja de la barra lateral derecha.
2. Haga clic en WAVE para mostrar el applet Waveform. Vuelva a hacer clic para ocultarlo.
3. Observe la visualización de la forma de onda. La traza se tiñe de color frío cuando se monitoriza audio de RX y de color cálido cuando se monitoriza audio de TX; no es necesario leer etiquetas.
4. Verifique la lectura del encabezado para conocer la dirección actual (RX o TX), el nivel RMS en dBFS y el nivel pico en dBFS.
5. Si no llega audio durante un segundo, la pantalla muestra un mensaje de marcador de posición en lugar de una traza vacía. Para la ruta RX, el mensaje dice **"Enable PC Audio"**. Para la ruta TX, dice **"no TX audio"**.
6. Para abrir el cajón de configuración, haga doble clic en cualquier lugar de la visualización de forma de onda. Vuelva a hacer doble clic para cerrarlo.
7. En el cajón de configuración, use el cuadro combinado View para elegir una visualización: **Scope**, **Envelope**, **History** o **Bands**. El valor predeterminado es **Scope**.
8. Use el control deslizante Zoom para escalar el eje de amplitud. El valor predeterminado es 1.7x (rango 1.0x–6.0x). Arrástrelo hacia la derecha para ampliar señales pequeñas; con valores de zoom altos, los artefactos de recorte aparecen antes.
9. Use el control deslizante FPS para establecer la frecuencia con la que se actualiza la pantalla (rango 5–30 Hz, predeterminado 24). Los valores más bajos reducen la carga de la CPU.
10. Use el control deslizante Window para establecer la ventana de tiempo mostrada. El control deslizante se detiene en pasos discretos: 240 ms, 480 ms, 1 s, luego incrementos de 1 segundo hasta 10 s. El valor predeterminado es 1 s.

## Función de cada control

| Control | Predeterminado | Rango válido | Clave persistida | Comportamiento |
|---|---|---|---|---|
| View | Scope | Scope, Envelope, History, Bands | `WaveApplet_ViewMode` | Selecciona el modo de visualización. Scope muestra la forma de onda mín./máx. y líneas RMS. Envelope muestra un área rellena de pico/RMS. History muestra barras de nivel horizontales. Bands muestra barras de bandas de frecuencia. |
| Zoom | 1.7x (170) | 1.0x–6.0x (100–600) | `WaveApplet_ZoomPercent` | Escala verticalmente el eje de amplitud. |
| FPS | 24 | 5–30 Hz | `WaveApplet_RefreshRateHz` | Controla la frecuencia de actualización. |
| Window | 1 s | 240 ms, 480 ms, 1 s, 2 s, 3 s, 4 s, 5 s, 6 s, 7 s, 8 s, 9 s, 10 s | `WaveApplet_TimeWindowMs` | Establece la ventana de tiempo mostrada en intervalos discretos escalonados. |
| Clic en la pantalla | En vivo | En vivo / Pausado | — | Alterna la pausa. Aparece una insignia PAUSED en el pie de página mientras la pantalla está congelada. |
| Doble clic en la pantalla | — | — | — | Abre o cierra el cajón de configuración. |

## Consejos

- Cuando se produce recorte, las columnas afectadas se resaltan y aparece un contador CLIP N en el encabezado. Reduzca el nivel de excitación de audio o disminuya el valor de Zoom para que la señal vuelva al rango.
- Haga clic una vez en la forma de onda para congelar una instantánea cuando observe un transitorio. Vuelva a hacer clic para reanudar la vista en vivo.
- El cajón de configuración se abre en estado expandido cada vez que inicia AetherSDR.
- El control deslizante Window usa pasos discretos en lugar de un ajuste continuo. Cada muesca proporciona un valor de ventana de tiempo específico. Los primeros tres pasos (240 ms, 480 ms, 1 s) ofrecen detalle de submilisegundos; los pasos restantes aumentan en incrementos de 1 segundo hasta 10 s.

## Solución de problemas

- **La pantalla muestra "Enable PC Audio"** — No han llegado muestras de alcance de RX en el último segundo. Asegúrese de que PC Audio esté habilitado en la configuración de audio de la radio. Verifique que el dispositivo de audio correcto esté seleccionado en `Settings > Radio Setup...`.
- **La pantalla muestra "no TX audio"** — No han llegado muestras de alcance de TX en el último segundo. Verifique que el audio fluya a través de la ruta de transmisión.
- **Falta el botón de bandeja WAVE** — El panel de applets puede estar oculto. Actívelo mediante `View > Applet Panel`. Si el panel está visible pero WAVE está ausente, use `View > Reset Applet Order` para restaurar la disposición predeterminada de applets.

## Relacionado

- [Resumen de forma de onda](overview.md)
- [Pausar la forma de onda para inspeccionar un transitorio](pause-the-waveform-to-inspect-a-transient.md)
- [Cambiar el modo de vista de forma de onda (Scope, Envelope, History, Bands)](switch-the-waveform-view-mode-scope-envelope-history-bands.md)
- [Ajustar el zoom de amplitud de la forma de onda](adjust-waveform-amplitude-zoom.md)
- [Establecer la frecuencia de actualización de la forma de onda para reducir la carga de CPU](set-the-waveform-refresh-rate-to-reduce-cpu-load.md)
- [Ajustar la ventana de tiempo de la forma de onda](adjust-the-waveform-time-window.md)
